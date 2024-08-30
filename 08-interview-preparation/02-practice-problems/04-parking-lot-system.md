# 04. Parking Lot System Practice Problem

## Overview

The parking lot system problem is a common technical interview question that tests a candidate's ability to design a system that efficiently manages parking spaces, including the allocation, tracking, and retrieval of information regarding parked vehicles. This problem assesses a candidate's understanding of object-oriented design, data structures, and system scalability. In this lesson, we will explore the problem statement, requirements, design considerations, and a sample implementation of a parking lot system.

## Problem Statement

Design a parking lot system that provides the following functionalities:

1. **Park a Vehicle**: Allow vehicles to be parked in the parking lot and assign them a parking spot.
2. **Retrieve Vehicle Information**: Allow users to retrieve information about parked vehicles based on their license plates or parking spot.
3. **Remove a Vehicle**: Enable users to remove a vehicle from the parking lot when it leaves.
4. **Display Available Spots**: Provide a way to display available parking spots in the lot.

## Requirements

### Functional Requirements

1. **Park Vehicle**:

   - Input: Vehicle details (e.g., license plate, vehicle type).
   - Output: A confirmation of successful parking and the assigned parking spot.

2. **Retrieve Vehicle Information**:

   - Input: License plate or parking spot.
   - Output: Details of the parked vehicle (e.g., license plate, vehicle type, parking spot).

3. **Remove Vehicle**:

   - Input: License plate or parking spot.
   - Output: A confirmation of successful removal or an error if the vehicle is not found.

4. **Display Available Spots**:
   - Output: A list of available parking spots.

### Non-Functional Requirements

1. **Scalability**: The system should be able to handle a large number of vehicles and parking spots efficiently.
2. **Performance**: Operations (park, retrieve, remove) should be performed quickly, with minimal latency.
3. **Data Persistence**: Store vehicle and parking spot information in a persistent storage solution.

## Design Considerations

### Data Storage

- **Data Structures**:
  - **Parking Spot**: Each parking spot can be represented as an object containing details like spot number, availability status, and vehicle type.
  - **Vehicle**: Each vehicle can be represented as an object containing details like license plate and vehicle type.

### Parking Lot Management

- **Parking Lot**: The parking lot can be represented as a collection of parking spots. Each parking spot can be tracked for availability.
- **Vehicle Type Handling**: Different vehicle types (e.g., compact, regular, oversized) may require different parking spots. The system should accommodate these variations.

### API Design

Design a simple API with the following endpoints:

1. **POST /park**

   - Request Body: `{ "licensePlate": "ABC123", "vehicleType": "compact" }`
   - Response: `{ "status": "success", "spot": "A1" }`

2. **GET /vehicle/{licensePlate}**

   - Request: `GET /vehicle/ABC123`
   - Response: `{ "licensePlate": "ABC123", "vehicleType": "compact", "spot": "A1" }` or an error if not found.

3. **DELETE /vehicle/{licensePlate}**

   - Request: `DELETE /vehicle/ABC123`
   - Response: `{ "status": "success" }` or an error if not found.

4. **GET /available-spots**
   - Request: `GET /available-spots`
   - Response: `{ "availableSpots": ["A2", "B1", "C3"] }`

## Implementation

### Example Implementation in Python

Here’s a simplified version of how you might implement a parking lot system in Python:

```python
class Vehicle:
    def __init__(self, license_plate, vehicle_type):
        self.license_plate = license_plate
        self.vehicle_type = vehicle_type

class ParkingSpot:
    def __init__(self, spot_number, vehicle_type=None):
        self.spot_number = spot_number
        self.vehicle_type = vehicle_type
        self.is_available = True if vehicle_type is None else False

class ParkingLot:
    def __init__(self):
        self.spots = {}
        self.vehicles = {}

    def add_spot(self, spot_number, vehicle_type=None):
        self.spots[spot_number] = ParkingSpot(spot_number, vehicle_type)

    def park_vehicle(self, license_plate, vehicle_type):
        for spot in self.spots.values():
            if spot.is_available and (spot.vehicle_type is None or spot.vehicle_type == vehicle_type):
                vehicle = Vehicle(license_plate, vehicle_type)
                self.vehicles[license_plate] = vehicle
                spot.is_available = False
                spot.vehicle_type = vehicle_type
                return f"Vehicle parked at spot {spot.spot_number}"
        return "No available spot for this vehicle type."

    def retrieve_vehicle(self, license_plate):
        vehicle = self.vehicles.get(license_plate)
        if vehicle:
            for spot in self.spots.values():
                if spot.vehicle_type == vehicle.vehicle_type and not spot.is_available:
                    return {
                        "licensePlate": vehicle.license_plate,
                        "vehicleType": vehicle.vehicle_type,
                        "spot": spot.spot_number
                    }
        return "Vehicle not found."

    def remove_vehicle(self, license_plate):
        vehicle = self.vehicles.pop(license_plate, None)
        if vehicle:
            for spot in self.spots.values():
                if spot.vehicle_type == vehicle.vehicle_type and not spot.is_available:
                    spot.is_available = True
                    spot.vehicle_type = None
                    return "Vehicle removed successfully."
        return "Vehicle not found."

    def available_spots(self):
        return [spot.spot_number for spot in self.spots.values() if spot.is_available]

# Example usage
parking_lot = ParkingLot()
parking_lot.add_spot("A1", "compact")
parking_lot.add_spot("A2", "compact")
parking_lot.add_spot("B1", "regular")

print(parking_lot.park_vehicle("ABC123", "compact"))  # Vehicle parked at spot A1
print(parking_lot.retrieve_vehicle("ABC123"))          # Vehicle details
print(parking_lot.remove_vehicle("ABC123"))            # Vehicle removed successfully
print(parking_lot.available_spots())                    # List of available spots
```

### Explanation of the Implementation

1. **Classes**:

   - **Vehicle**: Represents a vehicle with a license plate and type.
   - **ParkingSpot**: Represents a parking spot with a number, vehicle type, and availability status.
   - **ParkingLot**: Manages the collection of parking spots and vehicles.

2. **Methods**:
   - **add_spot**: Adds a new parking spot to the parking lot.
   - **park_vehicle**: Parks a vehicle in an available spot, considering vehicle type.
   - **retrieve_vehicle**: Retrieves the details of a parked vehicle based on the license plate.
   - **remove_vehicle**: Removes a vehicle from the parking lot and makes the spot available again.
   - **available_spots**: Returns a list of available parking spots.

## Conclusion

The parking lot system practice problem provides an excellent opportunity to demonstrate system design, object-oriented programming, and data management skills. By understanding the requirements, design considerations, and implementation details, candidates can effectively tackle this problem in a technical interview setting. Building a parking lot system not only tests a candidate's technical abilities but also their understanding of user interactions, data retrieval, and system scalability.
