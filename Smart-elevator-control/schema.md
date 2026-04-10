buildings[icon:building,color:blue]{
building_id serial pk
building_name text not null
floors int not null
created_at timestamp
updated_at timestamp
}

floors[icon:layers,color:blue]{
floor_id serial pk
floor_number int not null
building_id int fk
created_at timestamp
updated_at timestamp
}

shafts[icon:columns,color:blue]{
shaft_id serial pk
building_id int fk
created_at timestamp
updated_at timestamp
}

elevators[icon:arrow-up-down,color:blue]{
elevator_id serial pk
status text (idle, moving, maintenance) not null
shaft_id int fk not null
created_at timestamp
updated_at timestamp
}

zones[icon:map,color:purple]{
zone_id serial pk
zone_name text not null
start_floor_id int fk
end_floor_id int fk
building_id int fk
created_at timestamp
updated_at timestamp
}

elevator_zones[icon:link,color:purple]{
elevator_zone_id serial pk
zone_id int fk
elevator_id int fk
created_at timestamp
updated_at timestamp
}

requests[icon:bell,color:green]{
request_id serial pk
start_floor_id int fk
end_floor_id int fk
requested_at timestamp not null
created_at timestamp
updated_at timestamp
}

assigned_elevators[icon:check-circle,color:green]{
assigned_elevator_id serial pk
request_id int fk
elevator_id int fk
assigned_at timestamp not null
created_at timestamp
updated_at timestamp
}

ride_logs[icon:file-text,color:orange]{
ride_log_id serial pk
request_id int fk
assigned_elevator_id int fk
ride_status text (requested,assigned,travelling,reached) not null
start_time timestamp not null
end_time timestamp not null
created_at timestamp
updated_at timestamp
}

buildings.building_id < floors.building_id

zones.start_floor_id - floors.floor_id
zones.end_floor_id - floors.floor_id
buildings.building_id < zones.building_id

elevators.elevator_id < elevator_zones.elevator_id
zones.zone_id < elevator_zones.zone_id

buildings.building_id < shafts.building_id

requests.start_floor_id - floors.floor_id
requests.end_floor_id - floors.floor_id

assigned_elevators.request_id - requests.request_id
assigned_elevators.elevator_id - elevators.elevator_id

ride_logs.request_id - requests.request_id
ride_logs.assigned_elevator_id - assigned_elevators.assigned_elevator_id

elevators.shaft_id - shafts.shaft_id
