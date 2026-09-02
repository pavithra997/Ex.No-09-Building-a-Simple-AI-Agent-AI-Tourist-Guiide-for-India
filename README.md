# Ex.No-09-Building-a-Simple-AI-Agent-AI-Tourist-Guiide-for-India
## Aim : To design, implement and test a simple goal-based AI agent in Python that plans a personalised India trip itinerary for a tourist, based on the tourist's interest, trip duration and daily budget.
# OBJECTIVES
.To understand the concept of a goal-based Al agent..To implement the Perceive → Reason → Plan→Act cycle..To
create a knowledge base of Indian tourist destinations.To generate personalised itineraries based on interest, duration
and budget.. To test the agent with different tourist profiles.
# Introduction
An AI agent is anything that can perceive its environment through sensors and act upon that environment through actuators in order to achieve a specific goal. A useful way to describe an agent is the PEAS framework — Performance measure, Environment, Actuators and Sensors. Agents are commonly classified as simple reflex agents (react only to the current input), goal-based agents (choose actions that achieve a defined goal) and utility-based agents (choose the action that maximises a measure of “goodness”). In this experiment, an AI Tourist Agent for India is built as a goal-based agent: given a tourist's goal (an enjoyable trip within their interest and budget), the agent perceives the tourist's preferences, reasons over a knowledge base of Indian destinations, plans a day-wise itinerary, and acts by presenting the recommended plan.
# Procedure
### Step 1: Import Required Libraries
●	textwrap – used only to neatly wrap long destination descriptions to a fixed line width while printing the itinerary.
<img width="584" height="34" alt="image" src="https://github.com/user-attachments/assets/d7bd1246-346f-41f8-aec1-fddca7a8e120" />
### Step 2: Define the Agent's Knowledge Base (Destination Database)
●	The agent's environment knowledge is stored as a list of dictionaries, one per Indian destination.
●	Each destination has a category (heritage, spiritual, beach, hill_station, adventure, nature, wildlife), an estimated cost per day, the best travel season and a short description.
●	This knowledge base plays the same role for the agent that the environment model plays for any goal-based agent — it is what the agent reasons over to choose its actions.
<img width="619" height="236" alt="image" src="https://github.com/user-attachments/assets/4182dfe7-9114-4557-a80f-a8756a48b2f5" />
<img width="615" height="347" alt="image" src="https://github.com/user-attachments/assets/320ffc13-4890-4761-9499-34426c329b35" />
Destination Knowledge Base Summary
The table below summarises the destinations available to the agent:
<img width="673" height="213" alt="image" src="https://github.com/user-attachments/assets/c5fea0c9-95f2-482f-a1fb-d9cfafdcf2ea" />
### Step 3: Perceive — Read the Tourist's Goal / Preferences
●	The perceive() function represents the agent's sensors: it reads the tourist's profile (interest category, number of days, daily budget) and displays it back to confirm what was understood.
<img width="585" height="109" alt="image" src="https://github.com/user-attachments/assets/81c0cc39-ba1f-4736-8a51-1eb1ba2ff3f8" />
### Step 4: Reason — Filter and Rank Matching Destinations
●	The agent compares every destination in its knowledge base against the tourist's goal: same category and cost per day within the daily budget.
●	If nothing fits the exact budget, it falls back to all destinations of the requested category, sorted from cheapest to costliest, so the agent always tries to return a useful plan.
<img width="615" height="148" alt="image" src="https://github.com/user-attachments/assets/ba53e68e-5fb0-4673-83cf-5b705751df15" />
### Step 5: Plan — Build a Day-wise Itinerary
●	The agent allocates up to 3 days per destination and moves to the next matching destination once those days are used, cycling back to the first if needed for longer trips.
●	Consecutive days at the same destination are merged into a single itinerary block, and the total estimated cost is calculated as it plans.
<img width="612" height="290" alt="image" src="https://github.com/user-attachments/assets/f793c485-908e-4e98-84ca-119671909652" />
### Step 6: Act — Present the Recommendation to the Tourist
●	The act() function represents the agent's actuator: it prints a readable, day-wise itinerary with the destination, description, best season and cost for each leg of the trip, followed by the total estimated cost.
<img width="576" height="177" alt="image" src="https://github.com/user-attachments/assets/55712bdf-2b82-42b0-83f7-5b3eb7d94263" />
<img width="632" height="89" alt="image" src="https://github.com/user-attachments/assets/9a254225-96b6-4729-be35-29cac298c28d" />
### Step 7: The Agent Loop — Perceive → Reason → Plan → Act
●	run_agent() ties the four stages together into a single agent cycle, exactly as a real autonomous agent continuously perceives, reasons and acts within its environment.
<img width="432" height="89" alt="image" src="https://github.com/user-attachments/assets/0a46568e-9781-457b-8a10-e2a97a95c0a2" />
### Step 8: Test the Agent with Sample Tourist Profiles
●	Three realistic tourist profiles are used to test the agent across different interests and budgets: a budget heritage traveller, a mid-budget adventure seeker, and a family looking for a beach holiday.
<img width="616" height="241" alt="image" src="https://github.com/user-attachments/assets/17613086-5b61-44f1-8d85-cbbae85cfc4b" />
### Output
Agent Output – Session 1 (Budget Heritage Traveller)
●	The agent correctly perceives Ananya's preferences, reasons that Taj Mahal and Jaipur are the matching heritage destinations within budget, and plans a 6-day itinerary split evenly between them.
<img width="677" height="373" alt="image" src="https://github.com/user-attachments/assets/c92635bd-dffc-470d-ad75-2b8f806e3c70" />
Agent Output – Sessions 2 and 3 (Adventure Seeker and Beach Holiday)
●	For the adventure seeker, the agent plans a trip across Coorg and Spiti Valley, both within the Rs. 5,000/day budget.
●	For the beach-holiday family, the agent alternates between Goa and the Andaman Islands to fill all 7 requested days, and the total estimated cost is calculated automatically for each plan.
<img width="620" height="532" alt="image" src="https://github.com/user-attachments/assets/d0d7a414-912d-4768-8b4f-933a1037a4c6" />
Fig 2: Console output for the adventure-seeker and beach-holiday profiles, each with a complete itinerary and total cost.
## Conclusion
Thus, a simple goal-based AI Tourist Agent for India was successfully designed, implemented and tested using Python. The agent follows the classic Perceive → Reason → Plan → Act cycle: it perceives a tourist's goal (interest, duration and budget), reasons over a knowledge base of Indian destinations to find matching options, plans a day-wise itinerary, and acts by presenting a complete, costed trip recommendation. This experiment demonstrates the core building blocks of autonomous agents — environment knowledge, perception, reasoning/planning and action — on which more advanced AI agents (using machine learning, real-time APIs and large language models) are built.

