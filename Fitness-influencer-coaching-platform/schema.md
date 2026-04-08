users[icon:user, color: Blue]{
user_id serial pk
first_name text not null
last_name text not null
age int not null
initial_height float not null
initial_weight float not null
gender text ("male","female")  
 initial_body_fat_percentage float not null
email text unique not null
password text not null
created_at date not null
updated_at date not null
}
trainers[icon:user-check, color: Blue]{
trainer_id serial pk
first_name text not null
second_name text not null
age int not null
gender text ("male","female")  
 email text unique not null
password text not null
created_at date not null
updated_at date not null
}

subscription_plans[icon:map, color: Orange]{
subscription_plan_id serial pk
name text not null
fees int not null
duration int not null
description text not null
created_at date not null
updated_at date not null
}
user_subscriptions[icon:layers, color: Orange]{
user_subscription_id serial pk
user_id int fk
subscription_plan_id int fk
started_at date not null
expires_at date not null
status text not null (Active,Expired,Cancelled)
created_at date not null
updated_at date not null
}

sessions[icon:calendar, color: Yellow]{
session_id serial pk
name text not null
fees int not null
duration int not null
description text not null
start_date date not null
created_at date not null
updated_at date not null
}
user_sessions[icon:layers, color: Yellow]{
user_session_id serial pk
user_id int fk
session_id int fk
created_at date not null
updated_at date not null
}
trainer_notes[icon:edit, color: Purple] {
trainer_note_id serial pk
trainer_id int fk not null
user_id int fk not null
user_subscription_id int fk optional
user_session_id int fk optional
description text not null
created_at date not null
updated_at date not null
}
payments[icon:credit-card, color: Green]{
payment_id serial pk
user_session_id int fk null
user_subscription_id int fk null
payment_method text not null (COD,UPI,credit_card,debit_card,EMI)
provider_payment_id text unique not null
status text not null (pending,paid,partial)
created_at date not null
updated_at date not null
}
progress[icon:trending-up, color: Blue]{
progress_id serial pk
user_id int fk not null
weight float not null
height float not null
trainer_feedback text not null
body_fat_percentage float not null
created_at date not null
updated_at date not null
}

//relations
subscription_plans.subscription_plan_id < user_subscriptions.subscription_plan_id
users.user_id < user_subscriptions.user_id

users.user_id < user_sessions.user_id
sessions.session_id < user_sessions.session_id

trainers.trainer_id < trainer_notes.trainer_id
user_subscriptions.user_subscription_id < trainer_notes.user_subscription_id
user_sessions.user_session_id < trainer_notes.user_session_id
users.user_id < trainer_notes.user_id

payments.user_session_id - user_sessions.user_session_id
payments.user_subscription_id - user_subscriptions.user_subscription_id

users.user_id < progress.user_id
