vehicle [icon: car, color: blue] {
id int pk
number_plate text not null
vehicle_type_id int fk not null
created_at timestamp
updated_at timestamp
}

vehicle_type [icon: tag, color: purple] {
id int pk
name text not null
created_at timestamp
updated_at timestamp
}

zone [icon: map, color: orange] {
id int pk
name text not null
created_at timestamp
updated_at timestamp
}

level [icon: layers, color: orange] {
id int pk
zone_id int fk not null
level_number int not null
created_at timestamp
updated_at timestamp
}

spot_type [icon: grid, color: teal] {
id int pk
name text not null
created_at timestamp
updated_at timestamp
}

parking_spot [icon: square, color: teal] {
id int pk
spot_number text not null
level_id int fk not null
spot_type_id int fk not null
is_reserved boolean not null
created_at timestamp
updated_at timestamp
}

parking_session [icon: clock, color: red] {
id int pk
vehicle_id int fk not null
spot_id int fk not null
entry_time timestamp not null
exit_time timestamp
status text not null

created_at timestamp
updated_at timestamp
}

ticket [icon: ticket, color: green] {
id int pk
session_id int fk not null
ticket_number text not null
issued_at timestamp not null

created_at timestamp
updated_at timestamp
}

payment [icon: credit-card, color: green] {
id int pk
session_id int fk not null
amount decimal not null
payment_time timestamp not null
method text not null

created_at timestamp
updated_at timestamp
}

//relations
vehicle.vehicle_type_id > vehicle_type.id
level.zone_id > zone.id
parking_spot.level_id > level.id
parking_spot.spot_type_id > spot_type.id
parking_session.vehicle_id > vehicle.id
parking_session.spot_id > parking_spot.id
ticket.session_id > parking_session.id
payment.session_id > parking_session.id
