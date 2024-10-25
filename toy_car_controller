using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace RemoteCarController
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Compile_Click(object sender, EventArgs e)
        {
            // Define initial and final states
            string Initial_State = "Idle";
            string Final_State = "Stopped";

            // Define state transitions
            var stateMachine = new Dictionary<string, Dictionary<string, string>>();
            
            // Define transitions for each state
            stateMachine.Add("Idle", new Dictionary<string, string>()
            {
                { "Start", "Running" },
                { "Stop", "Stopped" },
                { "Accelerate", "Idle" }, // Invalid from Idle, remains Idle
            });
            
            stateMachine.Add("Running", new Dictionary<string, string>()
            {
                { "Accelerate", "Moving" },
                { "Stop", "Stopped" },
                { "Right", "TurningRight" },
                { "Left", "TurningLeft" }
            });
            
            stateMachine.Add("Moving", new Dictionary<string, string>()
            {
                { "Stop", "Stopped" },
                { "Right", "TurningRight" },
                { "Left", "TurningLeft" },
                { "Accelerate", "Moving" } // Continues moving
            });

            stateMachine.Add("TurningRight", new Dictionary<string, string>()
            {
                { "Stop", "Stopped" },
                { "Accelerate", "Moving" }
            });
            
            stateMachine.Add("TurningLeft", new Dictionary<string, string>()
            {
                { "Stop", "Stopped" },
                { "Accelerate", "Moving" }
            });

            string currentState = Initial_State;
            string[] commands = Input.Text.Split(' ');

            foreach (var command in commands)
            {
                if (stateMachine[currentState].ContainsKey(command))
                {
                    currentState = stateMachine[currentState][command];
                }
                else
                {
                    Output.Text = $"Error: '{command}' is not a valid command from state '{currentState}'.";
                    return;
                }
            }

            // Check if we reached the final state
            if (currentState == Final_State)
            {
                Output.Text = "RESULT OKAY";
            }
            else
            {
                Output.Text = "ERROR: Did not reach final state.";
            }
        }
    }
}
