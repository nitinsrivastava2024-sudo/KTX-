import enum
from datetime import datetime
from typing import Optional

from fastapi import FastAPI, Depends, HTTPException, status
from fastapi.middleware.cors import CORSMiddleware
from pydantic import BaseModel
from sqlalchemy import (
    create_engine,
    Column,
    Integer,
    String,
    Text,
    Float,
    Boolean,
    ForeignKey,
    DateTime,
    Enum,
)
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker, relationship, Session

# ==========================================
# 1. DATABASE CONFIGURATION & ENGINE
# ==========================================
DATABASE_URL = "sqlite:///./marketplace.db"

engine = create_engine(
    DATABASE_URL, connect_args={"check_same_thread": False}
)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

# ==========================================
# 2. DATABASE MODELS & SCHEMAS
# ==========================================
class UserRole(str, enum.Enum):
    CLIENT = "client"
    CONTRACTOR = "contractor"
    PROGRAMMER = "programmer"
    ENGINEER = "engineer"
    LABOR = "labor"
    DOCTOR = "doctor"
    TEACHER = "teacher"
    ADMIN = "admin"

class UserTier(str, enum.Enum):
    BRONZE = "Bronze"
    SILVER = "Silver"
    GOLD = "Gold"
    PLATINUM = "Platinum"

class ServiceCategory(str, enum.Enum):
    WEB_DEV = "Web Development"
    MOBILE_DEV = "Mobile App Development"
    GRAPHIC_DESIGN = "Graphic Design"
    PLUMBING_ELECTRICAL = "Plumbing & Electrical"
    HOME_REPAIR = "Home Repair & Construction"
    TUTORING = "Tutoring & Education"
    MEDICAL = "Medical Consultation"
    LEGAL = "Legal Advisory"

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True, index=True)
    phone = Column(String(15), unique=True, index=True, nullable=False)
    name = Column(String(100), default="New User")
    email = Column(String(100), unique=True, nullable=True)
    role = Column(Enum(UserRole), default=UserRole.CLIENT)
    tier = Column(Enum(UserTier), default=UserTier.BRONZE)
    rating = Column(Float, default=5.0)
    points = Column(Integer, default=100)
    is_verified = Column(Boolean, default=False)
    profile_bio = Column(Text, nullable=True)
    created_at = Column(DateTime, default=datetime.utcnow)

    services = relationship("Service", back_populates="owner")
    bids = relationship("Bid", back_populates="bidder")

class Service(Base):
    __tablename__ = "services"

    id = Column(Integer, primary_key=True, index=True)
    title = Column(String(200), index=True, nullable=False)
    category = Column(Enum(ServiceCategory), index=True, nullable=False)
    description = Column(Text, nullable=False)
    budget = Column(Float, nullable=False)
    location = Column(String(100), default="Remote / All India")
    is_active = Column(Boolean, default=True)
    created_at = Column(DateTime, default=datetime.utcnow)

    owner_id = Column(Integer, ForeignKey("users.id"))
    owner = relationship("User", back_populates="services")
    bids = relationship("Bid", back_populates="service")

class Bid(Base):
    __tablename__ = "bids"

    id = Column(Integer, primary_key=True, index=True)
    service_id = Column(Integer, ForeignKey("services.id"))
    bidder_id = Column(Integer, ForeignKey("users.id"))
    amount = Column(Float, nullable=False)
    proposal_text = Column(Text, nullable=False)
    created_at = Column(DateTime, default=datetime.utcnow)

    service = relationship("Service", back_populates="bids")
    bidder = relationship("User", back_populates="bids")

# Create all tables automatically
Base.metadata.create_all(bind=engine)

# ==========================================
# 3. PYDANTIC REQUEST SCHEMAS
# ==========================================
class SendOTPRequest(BaseModel):
    phone: str

class VerifyOTPRequest(BaseModel):
    phone: str
    otp: str
    role: Optional[UserRole] = UserRole.CLIENT
    name: Optional[str] = "Pro Member"

class ServiceCreateRequest(BaseModel):
    title: str
    category: ServiceCategory
    description: str
    budget: float
    location: str
    owner_id: int

class BidCreateRequest(BaseModel):
    service_id: int
    bidder_id: int
    amount: float
    proposal_text: str

# ==========================================
# 4. FASTAPI APP & ROUTES
# ==========================================
app = FastAPI(
    title="Enterprise Super Marketplace All-In-One",
    description="Unified backend engine for multi-category services",
    version="1.0.0"
)

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

@app.post("/api/auth/send-otp", tags=["Authentication"])
async def send_otp(req: SendOTPRequest):
    if len(req.phone) < 10:
        raise HTTPException(status_code=400, detail="Invalid mobile number")
    return {"status": "success", "message": "OTP sent successfully", "demo_otp": "1234"}

@app.post("/api/auth/verify-otp", tags=["Authentication"])
async def verify_otp(req: VerifyOTPRequest, db: Session = Depends(get_db)):
    if req.otp != "1234":
        raise HTTPException(status_code=400, detail="Invalid OTP code")
    
    user = db.query(User).filter(User.phone == req.phone).first()
    if not user:
        user = User(
            phone=req.phone,
            name=req.name,
            role=req.role,
            tier=UserTier.BRONZE,
            points=100
        )
        db.add(user)
        db.commit()
        db.refresh(user)
    
    return {
        "status": "success",
        "user": {
            "id": user.id,
            "name": user.name,
            "phone": user.phone,
            "role": user.role,
            "tier": user.tier,
            "points": user.points,
            "rating": user.rating
        }
    }

@app.post("/api/services", tags=["Marketplace"])
async def create_service(req: ServiceCreateRequest, db: Session = Depends(get_db)):
    service = Service(
        title=req.title,
        category=req.category,
        description=req.description,
        budget=req.budget,
        location=req.location,
        owner_id=req.owner_id
    )
    db.add(service)
    db.commit()
    db.refresh(service)
    return {"status": "success", "service_id": service.id, "message": "Service listed live"}

@app.get("/api/services", tags=["Marketplace"])
async def list_services(
    category: Optional[ServiceCategory] = None,
    location: Optional[str] = None,
    db: Session = Depends(get_db)
):
    query = db.query(Service).filter(Service.is_active == True)
    if category:
        query = query.filter(Service.category == category)
    if location:
        query = query.filter(Service.location.ilike(f"%{location}%"))
    
    services = query.order_by(Service.created_at.desc()).all()
    return {"count": len(services), "services": services}

@app.post("/api/bids", tags=["Marketplace"])
async def place_bid(req: BidCreateRequest, db: Session = Depends(get_db)):
    bid = Bid(
        service_id=req.service_id,
        bidder_id=req.bidder_id,
        amount=req.amount,
        proposal_text=req.proposal_text
    )
    db.add(bid)
    db.commit()
    return {"status": "success", "message": "Bid submitted to client"}

@app.get("/api/admin/analytics", tags=["Admin Panel"])
async def get_admin_metrics(admin_id: int, db: Session = Depends(get_db)):
    user = db.query(User).filter(User.id == admin_id).first()
    if not user or user.role != UserRole.ADMIN:
        raise HTTPException(status_code=403, detail="Unauthorized: Admin access only")
    
    total_users = db.query(User).count()
    total_services = db.query(Service).count()
    total_bids = db.query(Bid).count()
    
    return {
        "total_users": total_users,
        "total_services": total_services,
        "total_bids": total_bids,
        "platform_status": "Optimal (Zero Lag)"
    }

# ==========================================
# 5. SERVER ENTRYPOINT
# ==========================================
if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=8000)
    
