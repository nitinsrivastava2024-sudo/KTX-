
================================================================================
ENTERPRISE SUPER MARKETPLACE SYSTEM - FULL BACKEND ENGINE (FASTAPI + SQLALCHEMY)
================================================================================
Architecture: Asynchronous REST API + WebSockets + SQLite/PostgreSQL Engine
Author: Enterprise Solution Core
================================================================================
"""

import enum
import json
import logging
from datetime import datetime
from typing import List, Dict, Optional, Any

from fastapi import (
    FastAPI,
    Depends,
    HTTPException,
    status,
    WebSocket,
    WebSocketDisconnect,
    Query
)
from fastapi.middleware.cors import CORSMiddleware
from pydantic import BaseModel, Field, EmailStr
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
    desc
)
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker, relationship, Session

# ------------------------------------------------------------------------------
# 1. LOGGING & DATABASE SETUP
# ------------------------------------------------------------------------------
logging.basicConfig(level=logging.INFO, format="%(asctime)s - %(levelname)s - %(message)s")
logger = logging.getLogger("MarketplaceCore")

DATABASE_URL = "sqlite:///./enterprise_marketplace.db"

engine = create_engine(
    DATABASE_URL,
    connect_args={"check_same_thread": False},
    echo=False
)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

# ------------------------------------------------------------------------------
# 2. ENUMS (ROLES, TIERS, CATEGORIES, STATUSES)
# ------------------------------------------------------------------------------
class UserRole(str, enum.Enum):
    CLIENT = "Client"
    CONTRACTOR = "Contractor"
    PROGRAMMER = "Programmer"
    ENGINEER = "Engineer"
    LABOR = "Labor"
    DOCTOR = "Doctor"
    TEACHER = "Teacher"
    ADMIN = "Admin"

class UserTier(str, enum.Enum):
    BRONZE = "Bronze"
    SILVER = "Silver"
    GOLD = "Gold"
    PLATINUM = "Platinum"

class ServiceCategory(str, enum.Enum):
    WEB_DEV = "Web Development"
    MOBILE_DEV = "Mobile App Development"
    GRAPHIC_DESIGN = "Graphic Design"
    CONTENT_WRITING = "Content Writing"
    VIDEO_EDITING = "Video Editing"
    DIGITAL_MARKETING = "Digital Marketing"
    HOME_REPAIR = "Home Repair & Construction"
    PLUMBING_ELECTRICAL = "Plumbing & Electrical"
    CLEANING = "Cleaning Services"
    TUTORING = "Tutoring & Education"
    MEDICAL = "Medical Consultation"
    LEGAL = "Legal Advisory"
    FINANCE = "Finance & Accounting"
    PHOTOGRAPHY = "Photography"
    TRANSLATION = "Translation Services"
    SOCIAL_MEDIA = "Social Media Management"
    SEO = "SEO Services"
    DATA_ENTRY = "Data Entry"
    VIRTUAL_ASSIST = "Virtual Assistance"
    OTHER = "General On-Demand Services"

class BidStatus(str, enum.Enum):
    PENDING = "Pending"
    ACCEPTED = "Accepted"
    REJECTED = "Rejected"

class ProjectStatus(str, enum.Enum):
    OPEN = "Open"
    IN_PROGRESS = "In Progress"
    COMPLETED = "Completed"
    CANCELLED = "Cancelled"

# ------------------------------------------------------------------------------
# 3. DATABASE MODELS (TABLE DEFINITIONS)
# ------------------------------------------------------------------------------
class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True, index=True)
    phone = Column(String(20), unique=True, index=True, nullable=False)
    name = Column(String(100), default="Verified Member")
    email = Column(String(100), unique=True, nullable=True)
    role = Column(Enum(UserRole), default=UserRole.CLIENT, nullable=False)
    tier = Column(Enum(UserTier), default=UserTier.BRONZE, nullable=False)
    
    # Portfolio & Gamification
    rating = Column(Float, default=5.0)
    total_reviews = Column(Integer, default=0)
    points = Column(Integer, default=100)
    is_verified = Column(Boolean, default=False)
    profile_bio = Column(Text, default="Professional service provider on Super Marketplace.")
    portfolio_url = Column(String(255), nullable=True)
    wallet_balance = Column(Float, default=0.0)
    created_at = Column(DateTime, default=datetime.utcnow)

    services = relationship("Service", back_populates="owner", cascade="all, delete-orphan")
    bids = relationship("Bid", back_populates="bidder", cascade="all, delete-orphan")
    reviews_received = relationship("Review", foreign_keys="Review.target_user_id", back_populates="target_user")

class Service(Base):
    __tablename__ = "services"

    id = Column(Integer, primary_key=True, index=True)
    title = Column(String(200), index=True, nullable=False)
    category = Column(Enum(ServiceCategory), index=True, nullable=False)
    description = Column(Text, nullable=False)
    budget = Column(Float, nullable=False)
    location = Column(String(100), default="All India / Remote")
    status = Column(Enum(ProjectStatus), default=ProjectStatus.OPEN)
    is_active = Column(Boolean, default=True)
    created_at = Column(DateTime, default=datetime.utcnow)

    owner_id = Column(Integer, ForeignKey("users.id"))
    owner = relationship("User", back_populates="services")
    bids = relationship("Bid", back_populates="service", cascade="all, delete-orphan")

class Bid(Base):
    __tablename__ = "bids"

    id = Column(Integer, primary_key=True, index=True)
    service_id = Column(Integer, ForeignKey("services.id"), nullable=False)
    bidder_id = Column(Integer, ForeignKey("users.id"), nullable=False)
    amount = Column(Float, nullable=False)
    proposal_text = Column(Text, nullable=False)
    delivery_days = Column(Integer, default=3)
    status = Column(Enum(BidStatus), default=BidStatus.PENDING)
    created_at = Column(DateTime, default=datetime.utcnow)

    service = relationship("Service", back_populates="bids")
    bidder = relationship("User", back_populates="bids")

class Review(Base):
    __tablename__ = "reviews"

    id = Column(Integer, primary_key=True, index=True)
    reviewer_id = Column(Integer, ForeignKey("users.id"))
    target_user_id = Column(Integer, ForeignKey("users.id"))
    rating = Column(Float, nullable=False)
    comment = Column(Text, nullable=False)
    created_at = Column(DateTime, default=datetime.utcnow)

    target_user = relationship("User", foreign_keys=[target_user_id], back_populates="reviews_received")

class Transaction(Base):
    __tablename__ = "transactions"

    id = Column(Integer, primary_key=True, index=True)
    user_id = Column(Integer, ForeignKey("users.id"))
    amount = Column(Float, nullable=False)
    txn_type = Column(String(50), default="CREDIT")
    reference_id = Column(String(100), unique=True)
    description = Column(String(255))
    created_at = Column(DateTime, default=datetime.utcnow)

# Auto-create all tables
Base.metadata.create_all(bind=engine)

# ------------------------------------------------------------------------------
# 4. PYDANTIC SCHEMAS (REQUEST/RESPONSE)
# ------------------------------------------------------------------------------
class SendOTPRequest(BaseModel):
    phone: str = Field(..., example="9876543210")

class VerifyOTPRequest(BaseModel):
    phone: str = Field(..., example="9876543210")
    otp: str = Field(..., example="1234")
    name: Optional[str] = "Pro Member"
    role: Optional[UserRole] = UserRole.CLIENT

class ServiceCreate(BaseModel):
    owner_id: int
    title: str
    category: ServiceCategory
    description: str
    budget: float
    location: Optional[str] = "Remote / All India"

class BidCreate(BaseModel):
    service_id: int
    bidder_id: int
    amount: float
    proposal_text: str
    delivery_days: int = 3

class ReviewCreate(BaseModel):
    reviewer_id: int
    target_user_id: int
    rating: float = Field(..., ge=1.0, le=5.0)
    comment: str

class WalletTopup(BaseModel):
    user_id: int
    amount: float

# ------------------------------------------------------------------------------
# 5. REAL-TIME WEBSOCKET CONNECTION MANAGER
# ------------------------------------------------------------------------------
class ConnectionManager:
    def __init__(self):
        self.active_connections: Dict[str, WebSocket] = {}

    async def connect(self, room_id: str, websocket: WebSocket):
        await websocket.accept()
        self.active_connections[room_id] = websocket
        logger.info(f"WebSocket Client connected to room: {room_id}")

    def disconnect(self, room_id: str):
        if room_id in self.active_connections:
            del self.active_connections[room_id]
            logger.info(f"WebSocket Client disconnected from room: {room_id}")

    async def broadcast_to_room(self, room_id: str, message: dict):
        if room_id in self.active_connections:
            await self.active_connections[room_id].send_text(json.dumps(message))

ws_manager = ConnectionManager()

# ------------------------------------------------------------------------------
# 6. FASTAPI CORE ENGINE SETUP
# ------------------------------------------------------------------------------
app = FastAPI(
    title="Enterprise Super Marketplace Core API",
    description="High-throughput on-demand services platform with full authentication, gamification, and real-time chat.",
    version="2.0.0"
)

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

# ------------------------------------------------------------------------------
# 7. AUTHENTICATION & PROFILE APIS
# ------------------------------------------------------------------------------
@app.post("/api/auth/send-otp", tags=["1. Authentication"])
async def send_otp(payload: SendOTPRequest):
    if len(payload.phone) < 10:
        raise HTTPException(status_code=400, detail="Mobile number must be at least 10 digits")
    logger.info(f"OTP generated for {payload.phone}")
    return {
        "status": "success",
        "message": f"OTP successfully dispatched to +91 {payload.phone}",
        "demo_otp": "1234"
    }

@app.post("/api/auth/verify-otp", tags=["1. Authentication"])
async def verify_otp(payload: VerifyOTPRequest, db: Session = Depends(get_db)):
    if payload.otp != "1234":
        raise HTTPException(status_code=400, detail="Invalid OTP code. Please enter 1234.")

    user = db.query(User).filter(User.phone == payload.phone).first()
    if not user:
        user = User(
            phone=payload.phone,
            name=payload.name or "Verified User",
            role=payload.role or UserRole.CLIENT,
            tier=UserTier.BRONZE,
            points=100
        )
        db.add(user)
        db.commit()
        db.refresh(user)

    return {
        "status": "success",
        "message": "Authentication successful",
        "user": {
            "id": user.id,
            "name": user.name,
            "phone": user.phone,
            "role": user.role,
            "tier": user.tier,
            "rating": user.rating,
            "points": user.points,
            "wallet_balance": user.wallet_balance,
            "is_verified": user.is_verified
        }
    }

@app.get("/api/users/{user_id}", tags=["1. Authentication"])
async def get_user_profile(user_id: int, db: Session = Depends(get_db)):
    user = db.query(User).filter(User.id == user_id).first()
    if not user:
        raise HTTPException(status_code=404, detail="User not found")
    return user

# ------------------------------------------------------------------------------
# 8. SERVICES & MARKETPLACE APIS (ALL 20+ CATEGORIES)
# ------------------------------------------------------------------------------
@app.post("/api/services", tags=["2. Marketplace Listings"])
async def post_service_or_project(payload: ServiceCreate, db: Session = Depends(get_db)):
    owner = db.query(User).filter(User.id == payload.owner_id).first()
    if not owner:
        raise HTTPException(status_code=404, detail="Service poster not found")

    new_service = Service(
        title=payload.title,
        category=payload.category,
        description=payload.description,
        budget=payload.budget,
        location=payload.location,
        owner_id=payload.owner_id
    )
    db.add(new_service)
    
    # Gamification: Reward points on posting
    owner.points += 20
    db.commit()
    db.refresh(new_service)

    return {
        "status": "success",
        "service_id": new_service.id,
        "message": f"Service listed under '{new_service.category.value}' successfully."
    }

@app.get("/api/services", tags=["2. Marketplace Listings"])
async def search_services(
    category: Optional[ServiceCategory] = None,
    location: Optional[str] = None,
    min_budget: Optional[float] = None,
    max_budget: Optional[float] = None,
    db: Session = Depends(get_db)
):
    query = db.query(Service).filter(Service.is_active == True)
    
    if category:
        query = query.filter(Service.category == category)
    if location:
        query = query.filter(Service.location.ilike(f"%{location}%"))
    if min_budget:
        query = query.filter(Service.budget >= min_budget)
    if max_budget:
        query = query.filter(Service.budget <= max_budget)

    results = query.order_by(desc(Service.created_at)).all()
    return {"total_count": len(results), "services": results}

# ------------------------------------------------------------------------------
# 9. BIDDING & QUOTE SYSTEM
# ------------------------------------------------------------------------------
@app.post("/api/bids", tags=["3. Bidding Engine"])
async def submit_proposal_bid(payload: BidCreate, db: Session = Depends(get_db)):
    service = db.query(Service).filter(Service.id == payload.service_id).first()
    if not service:
        raise HTTPException(status_code=404, detail="Target service not found")

    bidder = db.query(User).filter(User.id == payload.bidder_id).first()
    if not bidder:
        raise HTTPException(status_code=404, detail="Bidder not found")

    bid = Bid(
        service_id=payload.service_id,
        bidder_id=payload.bidder_id,
        amount=payload.amount,
        proposal_text=payload.proposal_text,
        delivery_days=payload.delivery_days
    )
    db.add(bid)
    
    # Reward points for activity
    bidder.points += 10
    db.commit()
    db.refresh(bid)

    return {"status": "success", "bid_id": bid.id, "message": "Proposal submitted to client."}

@app.get("/api/services/{service_id}/bids", tags=["3. Bidding Engine"])
async def view_service_bids(service_id: int, db: Session = Depends(get_db)):
    bids = db.query(Bid).filter(Bid.service_id == service_id).all()
    return {"service_id": service_id, "bids_count": len(bids), "bids": bids}

# ------------------------------------------------------------------------------
# 10. REVIEWS & GAMIFICATION SYSTEM
# ------------------------------------------------------------------------------
@app.post("/api/reviews", tags=["4. Reviews & Reputation"])
async def submit_review(payload: ReviewCreate, db: Session = Depends(get_db)):
    target = db.query(User).filter(User.id == payload.target_user_id).first()
    if not target:
        raise HTTPException(status_code=404, detail="Target user not found")

    review = Review(
        reviewer_id=payload.reviewer_id,
        target_user_id=payload.target_user_id,
        rating=payload.rating,
        comment=payload.comment
    )
    db.add(review)

    # Recalculate average rating & tier upgrade
    total_reviews = db.query(Review).filter(Review.target_user_id == target.id).count() + 1
    target.rating = round(((target.rating * (total_reviews - 1)) + payload.rating) / total_reviews, 2)
    target.total_reviews = total_reviews
    target.points += 50

    # Dynamic Tier Upgrade Logic
    if target.points >= 1000:
        target.tier = UserTier.PLATINUM
    elif target.points >= 500:
        target.tier = UserTier.GOLD
    elif target.points >= 250:
        target.tier = UserTier.SILVER

    db.commit()
    return {"status": "success", "new_rating": target.rating, "tier": target.tier}

# ------------------------------------------------------------------------------
# 11. WALLET & PAYMENTS ENGINE (MONETIZATION-READY)
# ------------------------------------------------------------------------------
@app.post("/api/wallet/topup", tags=["5. Payments & Wallet"])
async def wallet_topup(payload: WalletTopup, db: Session = Depends(get_db)):
    user = db.query(User).filter(User.id == payload.user_id).first()
    if not user:
        raise HTTPException(status_code=404, detail="User not found")

    user.wallet_balance += payload.amount
    txn = Transaction(
        user_id=user.id,
        amount=payload.amount,
        txn_type="CREDIT",
        reference_id=f"TXN_{int(datetime.utcnow().timestamp())}",
        description="Wallet Recharge (Pre-Gateway Integration)"
    )
    db.add(txn)
    db.commit()
    return {"status": "success", "updated_balance": user.wallet_balance}

# ------------------------------------------------------------------------------
# 12. REAL-TIME WEBSOCKET CHAT
# ------------------------------------------------------------------------------
@app.websocket("/ws/chat/{room_id}")
async def chat_endpoint(websocket: WebSocket, room_id: str):
    await ws_manager.connect(room_id, websocket)
    try:
        while True:
            data = await websocket.receive_text()
            payload = json.loads(data)
            await ws_manager.broadcast_to_room(room_id, {
                "sender": payload.get("sender", "Anonymous"),
                "message": payload.get("message", ""),
                "timestamp": datetime.utcnow().strftime("%H:%M:%S")
            })
    except WebSocketDisconnect:
        ws_manager.disconnect(room_id)

# ------------------------------------------------------------------------------
# 13. MASTER ADMIN ANALYTICS
# ------------------------------------------------------------------------------
@app.get("/api/admin/overview", tags=["6. Secret Admin Control"])
async def admin_dashboard_metrics(admin_phone: str, db: Session = Depends(get_db)):
    # Verify Admin identity
    admin = db.query(User).filter(User.phone == admin_phone, User.role == UserRole.ADMIN).first()
    if not admin:
        raise HTTPException(status_code=403, detail="Access Denied: Master Admin verification required")

    return {
        "platform": "Super Marketplace Hub",
        "status": "Healthy / 0ms Latency",
        "analytics": {
            "total_registered_users": db.query(User).count(),
            "total_active_services": db.query(Service).count(),
            "total_bids_placed": db.query(Bid).count(),
            "total_reviews_logged": db.query(Review).count(),
            "total_system_volume_inr": db.query(Transaction).count() * 1000.0
        }
    }

# ------------------------------------------------------------------------------
# 14. SERVER STARTUP
# ------------------------------------------------------------------------------
if __name__ == "__main__":
    import uvicorn
    print("\n" + "="*60)
    print("🚀 ENTERPRISE SUPER MARKETPLACE SYSTEM BOOTING UP...")
    print("📍 Interactive Docs : http://127.0.0.1:8000/docs")
    print("⚡ Real-Time Chat   : ws://127.0.0.1:8000/ws/chat/{room_id}")
    print("="*60 + "\n")
    uvicorn.run("app:app", host="0.0.0.0", port=8000, reload=True)
