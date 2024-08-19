# Smart_Irrigation


The project described in the code is a **Solar Tracking and Soil Moisture Control System**. It combines two functionalities:

1. **Solar Tracking System**:
   - This system uses two Light Dependent Resistors (LDRs) to track the position of the sun.
   - Based on the difference in light intensity detected by the LDRs, a servo motor adjusts the position of a solar panel to optimize its angle towards the sun.
   - The angle adjustment is constrained between 0 and 180 degrees to prevent over-rotation.

2. **Soil Moisture Control System**:
   - A soil moisture sensor monitors the moisture level in the soil.
   - If the soil is dry, the system activates a relay that could, for example, turn on a water pump to irrigate the soil.
   - If the soil is sufficiently moist, the relay remains off.

The system continuously monitors and adjusts the solar panel position and soil moisture level, with a short delay between each cycle.
