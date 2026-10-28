# Database Schema Design

## 1. users
- `id`: UUID (Primary Key)
- `email`: VARCHAR(255), Unique, Not Null
- `hashed_password`: VARCHAR(255), Not Null
- `full_name`: VARCHAR(100), Not Null
- `role`: ENUM ('member', 'coach', 'admin'), Default 'member'
- `created_at`: TIMESTAMPTZ, Default NOW()

## 2. memberships
- `id`: UUID (Primary Key)
- `user_id`: UUID (Foreign Key -> users.id)
- `plan_name`: VARCHAR(50) (e.g., 'Monthly Basic', 'Annual VIP')
- `status`: ENUM ('active', 'inactive', 'cancelled')
- `start_date`: DATE
- `end_date`: DATE

## 3. classes
- `id`: UUID (Primary Key)
- `title`: VARCHAR(100) (e.g., 'Spin Class', 'Powerlifting 101')
- `coach_name`: VARCHAR(100)
- `capacity`: INTEGER, Check (capacity > 0)
- `start_time`: TIMESTAMPTZ
- `duration_minutes`: INTEGER

## 4. bookings
- `id`: UUID (Primary Key)
- `class_id`: UUID (Foreign Key -> classes.id)
- `user_id`: UUID (Foreign Key -> users.id)
- `status`: ENUM ('confirmed', 'cancelled')
- `booked_at`: TIMESTAMPTZ, Default NOW()
- **Constraint:** UNIQUE(user_id, class_id) to prevent duplicate bookings