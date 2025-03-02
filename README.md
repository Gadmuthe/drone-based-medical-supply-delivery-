import time
import random 

class MedicalDrone:
    def __init__(self, max_payload=1.0, battery_capacity=100, range_km=10):
        self.max_payload = max_payload  # kg
        self.battery_capacity = battery_capacity  # %
        self.range_km = range_km
        self.current_location = "Base"
        self.destination = None
        self.is_flying = False
        self.payload_weight = 0.0

    def load_payload(self, weight):
        if weight > self.max_payload:
            print("Error: Payload exceeds maximum capacity!")
            return False
        self.payload_weight = weight
        print(f"Payload of {weight}kg loaded successfully.")
        return True

    def set_destination(self, location):
        if self.is_flying:
            print("Error: Cannot set destination while in flight!")
            return
        self.destination = location
        print(f"Destination set to {location}.")

    def check_battery(self):
        print(f"Battery level: {self.battery_capacity}%")
        return self.battery_capacity > 50  # Minimum battery required for flight

    def fly(self):
        if not self.destination:
            print("Error: No destination set!")
            return
        if self.payload_weight == 00:
            print("Error: No payload loaded!")
            return
        if not self.check_battery():
            print("Error: Insufficient battery!")
            return

        print(f"Flying to {self.destination}...")
        self.is_flying = True
        time.sleep(random.randint(2, 5))  # Simulating flight time
        self.current_location = self.destination
        self.is_flying = False
        self.battery_capacity -= random.randint(10, 20)  # Battery consumption
        print(f"Arrived at {self.destination}. Payload delivered successfully!")
        self.payload_weight = 0.0
        self.destination = None

    def return_to_base(self):
        if self.current_location == "Base":
            print("Drone is already at the base.")
            return
        if not self.check_battery():
            print("Error: Insufficient battery to return to base!")
            return

        print("Returning to base...")
        self.is_flying = True
        time.sleep(random.randint(2, 5))
        self.current_location = "Base"
        self.is_flying = False
        self.battery_capacity -= random.randint(10, 20)
        print("Drone has returned to base safely.")

# Example usage
drone = MedicalDrone()
drone.load_payload(0.8)
drone.set_destination("Hospital A")
drone.fly()
drone.return_to_base()
