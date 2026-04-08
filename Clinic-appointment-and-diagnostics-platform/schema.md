doctors[icon:stethoscope, color: Blue]{
doctor_id serial pk
first_name text not null
last_name text not null
phone_number text unique not null
email text unique not null
password text not null
is_active boolean default true not null
gender text not null (male,female)
date_of_birth date not null
qualification text optional
experience_years int optional
created_at timestamp not null
updated_at timestamp not null
}

patients[icon:user, color: Blue]{
patient_id serial pk
first_name text not null
last_name text not null
phone_number text unique not null
email text unique not null
password text not null
gender text not null (male,female)
date_of_birth date optional
blood_group text optional
created_at timestamp not null
updated_at timestamp not null
}
appointments[icon:calendar, color: yellow]{
appointment_id serial pk
patient_id int fk
doctor_id int fk
appointment_time timestamp
cause_description text not null
status text not null (pending,confirmed,cancelled,completed)
}
consultations[icon:activity, color: green] {
consultation_id serial pk
appointment_id int fk unique
start_time timestamp
end_time timestamp
notes text optional
status text not null ('ongoing', 'completed')
fee int not null
created_at timestamp not null
updated_at timestamp not null
}
diagnostics[icon:flask, color: green]{
diagnostic_id serial pk
consultation_id int fk
test_name text not null
instructions text optional
status text not null (prescribed, in_progress, completed)
requested_at timestamp
completed_at timestamp
created_at timestamp not null
updated_at timestamp not null
}
prescriptions[icon:file-text, color: green]{
prescription_id serial pk
consultation_id int fk
notes text optional
created_at timestamp not null
updated_at timestamp not null
}
prescription_items[icon:pill, color: green] {
prescription_items_id serial pk
prescription_id int fk
medicine_name text not null
dosage text not null
frequency text not null
duration text not null
instructions text optional
created_at timestamp not null
updated_at timestamp not null
}
reports[icon:file, color: orange]{
report_id serial pk
diagnostic_id int fk
fee int not null
note text optional
report_url text not null
created_at timestamp not null
updated_at timestamp not null
}
payments [icon:credit-card, color: yellow]{
payment_id serial pk
patient_id int fk not null
consultation_id int fk null
provider text not null
provider_payment_id text unique not null
status text not null (pending,paid)
}
payment_items [icon:receipt, color: yellow]{
payment_item_id serial pk
payment_id int fk

item_type text not null ('consultation', 'diagnostic')

item_id int not null
amount int not null
created_at timestamp not null
updated_at timestamp not null
}
specialties[icon:tag, color: purple] {
specialty_id serial pk
name text unique not null
description text optional
created_at timestamp not null
updated_at timestamp not null
}
doctor_specialties[icon:link, color: purple] {
doctor_specialty_id serial pk
doctor_id int fk
specialty_id int fk
created_at timestamp not null
updated_at timestamp not null
}

//relations
patients.patient_id < appointments.patient_id

doctors.doctor_id < appointments.doctor_id

consultations.appointment_id - appointments.appointment_id

consultations.consultation_id < diagnostics.consultation_id

consultations.consultation_id < prescriptions.consultation_id

prescriptions.prescription_id < prescription_items.prescription_id

diagnostics.diagnostic_id - reports.diagnostic_id

consultations.consultation_id - payments.consultation_id

patients.patient_id < payments.patient_id

payments.payment_id < payment_items.payment_id

doctors.doctor_id < doctor_specialties.doctor_id

specialties.specialty_id < doctor_specialties.specialty_id
