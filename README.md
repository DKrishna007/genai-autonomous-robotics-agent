# GenAI Autonomous Robotics Agent

LLM-powered autonomous robotics agent that parses natural language commands into ROS 2 Nav2 goals. Achieves ~90% task success rate and 120-180ms command-to-execution latency.

## Features

- Natural language command parsing (rule-based + OpenAI LLM)
- - ROS 2 Nav2 action client integration
  - - Simulation mode (no ROS 2 required for testing)
    - - Named location map with configurable waypoints
      - - Performance statistics tracking
        - - Batch command execution with JSON output
         
          - ## Quick Start
         
          - ### 1. Clone the repository
          - ```bash
            git clone https://github.com/DKrishna007/genai-autonomous-robotics-agent.git
            cd genai-autonomous-robotics-agent
            ```

            ### 2. Install dependencies
            ```bash
            pip install -r requirements.txt
            ```

            ### 3. Run in demo mode (no ROS 2 needed)
            ```bash
            python agent.py --mode demo --sim
            ```

            ### 4. Run interactively
            ```bash
            python agent.py --mode interactive --sim
            ```

            ### 5. Run with OpenAI LLM (requires API key)
            ```bash
            export OPENAI_API_KEY=your_key_here
            python agent.py --mode interactive --use-llm
            ```

            ### 6. Run batch commands
            ```bash
            python agent.py --mode batch --commands-file sample_commands.txt --sim
            ```

            ## Example Commands

            ```
            Go to the kitchen
            Navigate to bedroom
            Take me to the charging station
            Move to the living room
            Go to coordinates 2.5 3.0
            Navigate to the entrance
            ```

            ## Available Locations

            | Location | X | Y | Description |
            |----------|---|---|-------------|
            | kitchen | 2.5 | 1.0 | Kitchen area |
            | living room | 0.0 | 0.0 | Living room |
            | bedroom | -2.0 | 3.0 | Bedroom |
            | bathroom | 3.0 | 4.0 | Bathroom |
            | entrance | 0.0 | -3.0 | Front door |
            | charging station | 1.0 | -1.5 | Charging dock |

            ## Architecture

            ```
            NL Command -> CommandParser -> NavigationGoal -> ROS2 Nav2
                              |
                       [LLM / Rules]
            ```

            ## Performance Results

            See `outputs/demo_results.json` for sample benchmark results:
            - Success rate: ~90%
            - - Avg latency: 120-180ms
              - - Locations parsed: 10+ named rooms + coordinate commands
               
                - ## ROS 2 Setup
               
                - ```bash
                  # Ubuntu 22.04 + ROS 2 Humble
                  sudo apt install ros-humble-desktop ros-humble-nav2-bringup
                  source /opt/ros/humble/setup.bash
                  python agent.py --mode interactive
                  ```

                  ## Project Structure

                  ```
                  genai-autonomous-robotics-agent/
                  ├── agent.py              # Main agent implementation
                  ├── requirements.txt      # Python dependencies
                  ├── sample_commands.txt   # Example command inputs
                  ├── outputs/
                  │   └── demo_results.json # Sample benchmark results
                  └── README.md
                  ```
                  
