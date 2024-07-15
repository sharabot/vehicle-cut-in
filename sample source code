import numpy as np
host_vehicle_position = np.array([0, 0])  # Assume the host vehicle is at the origin

# Simulate positions and velocities of other vehicles
vehicles = [
    {"position": np.array([10, 2]), "velocity": np.array([-1, 0])},  # Vehicle 1
    {"position": np.array([8, -2]), "velocity": np.array([-1, 0.5])},  # Vehicle 2
    {"position": np.array([15, 1]), "velocity": np.array([-2, 0])},  # Vehicle 3
]

# Parameters
cut_in_threshold_distance = 1.5  # Distance threshold for considering a cut-in
time_threshold_min = 0.5  # Minimum time threshold in seconds
time_threshold_max = 0.7  # Maximum time threshold in seconds
time_step = 0.1  # Time step for simulation

def predict_position(vehicle, time):
    """Predict the position of a vehicle at a given time in the future."""
    return vehicle["position"] + vehicle["velocity"] * time
def detect_cut_in(host_position, vehicles, distance_threshold, time_min, time_max):
    """Detect if any vehicle cuts into the lane in front of the host vehicle within a specified time range."""
    for vehicle in vehicles:
        for t in np.arange(time_min, time_max + time_step, time_step):
            predicted_position = predict_position(vehicle, t)
            distance = np.linalg.norm(predicted_position - host_position)
            # Check if the vehicle is within the threshold distance and in the same lane (y = 0)
            if distance < distance_threshold and predicted_position[1] == 0:
                return True, predicted_position, t
    return False, None, None

# Run the detection
cut_in_detected, cut_in_position, cut_in_time = detect_cut_in(
    host_vehicle_position, vehicles, cut_in_threshold_distance, time_threshold_min, time_threshold_max
)

if cut_in_detected:
    print(f"Cut-in detected at position {cut_in_position} at time {cut_in_time}")
else:
    print("No cut-in detected within the specified time threshold")
