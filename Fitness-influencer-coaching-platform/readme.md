# Fitness Coaching Platform Database

A database design for an online fitness coaching platform where trainers manage clients, sell subscription plans, conduct sessions, track progress, and handle payments.

---

## 🚀 Features

- User (client) and trainer management
- Subscription plans with duration and pricing
- Session-based consultations
- User enrollments in plans and sessions
- Trainer notes for personalized coaching
- Payment tracking for subscriptions and sessions
- Progress tracking (weight, body fat, feedback)

---

## 📦 Core Entities

### Users

Stores client information like name, age, gender, and initial fitness data such as height, weight, and body fat percentage.

### Trainers

Stores trainer details who guide users through plans, sessions, and overall coaching.

### Subscription Plans

Defines long-term coaching programs including fees, duration, and description.

### User Subscriptions

Tracks which user has enrolled in which subscription plan, including start date, expiry date, and status (Active, Expired, Cancelled).

### Sessions

Represents one-time or short-term consultations or training sessions scheduled on specific dates.

### User Sessions

Maps users to sessions they have enrolled in.

### Trainer Notes

Stores personalized notes given by trainers to users.  
Each note can optionally be linked to a subscription or a session.

### Payments

Tracks payments made for subscriptions or sessions, including payment method, provider payment ID, and status.

### Progress

Tracks user fitness updates over time such as weight, height, body fat percentage, and trainer feedback.

---

## 🔗 Relationships

- User → User Subscriptions (1:M)
- User → User Sessions (1:M)
- User → Trainer Notes (1:M)
- User → Progress (1:M)

- Trainer → Trainer Notes (1:M)

- Subscription Plan → User Subscriptions (1:M)

- Session → User Sessions (1:M)

- User Subscription → Payments (1:M)
- User Session → Payments (1:M)

---

## 🧠 Notes

- A user can purchase multiple subscription plans over time.
- A user can attend multiple sessions.
- Trainer notes provide personalized feedback and may be linked to either subscriptions or sessions.
- Payments are flexible and support both subscription-based and session-based transactions.
- Progress is tracked over time to monitor user fitness improvements.
