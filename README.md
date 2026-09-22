# Ex.No-09-Building-a-Simple-AI-Agent-AI-Tourist-Guiide-for-India
## Aim 
To design, implement and test a simple goal-based AI agent in Python that plans a personalised India trip itinerary for a tourist, based on the tourist's interest, trip duration and daily budget.
# OBJECTIVES
To understand the concept of a goal-based Al agent..To implement the Perceive → Reason → Plan→Act cycle..To
create a knowledge base of Indian tourist destinations.To generate personalised itineraries based on interest, duration
and budget.. To test the agent with different tourist profiles.
# Introduction
An AI agent is anything that can perceive its environment through sensors and act upon that environment through actuators in order to achieve a specific goal. A useful way to describe an agent is the PEAS framework — Performance measure, Environment, Actuators and Sensors. Agents are commonly classified as simple reflex agents (react only to the current input), goal-based agents (choose actions that achieve a defined goal) and utility-based agents (choose the action that maximises a measure of “goodness”). In this experiment, an AI Tourist Agent for India is built as a goal-based agent: given a tourist's goal (an enjoyable trip within their interest and budget), the agent perceives the tourist's preferences, reasons over a knowledge base of Indian destinations, plans a day-wise itinerary, and acts by presenting the recommended plan.
# Procedure
```
Step 1: Import Required Library
Import the textwrap library to format and display long destination descriptions neatly.

Step 2: Define the Knowledge Base
Create a list called destinations containing information about Indian tourist destinations.

Each destination contains:

Name

State

Category

Cost per day

Best season

Description

Step 3: Perceive – Read Tourist Preferences
Create the perceive() function.

It reads the tourist profile such as:

Tourist name

Interest/category

Number of days

Daily budget

The profile is then returned for further processing.

Step 4: Reason – Find Matching Destinations
Create the reason() function.

The agent:

Checks the tourist's preferred category.

Checks whether the destination cost is within the daily budget.

Selects matching destinations.

If no destination fits the budget, it selects all destinations from the requested category.

Sorts the destinations according to cost.

Step 5: Plan – Create the Itinerary
Create the plan() function.

The agent:

Reads the number of travel days.

Allocates a maximum of 3 days to each destination.

Moves to the next matching destination.

Calculates the total estimated trip cost.

Step 6: Act – Display the Recommendation
Create the act() function.

It displays:

Day-wise itinerary

Destination name

State

Description

Best season

Cost per day

Total estimated trip cost

Step 7: Run the Agent
Create the run_agent() function.

The four stages are connected:

Perceive → Reason → Plan → Act

Step 8: Test the Agent
Create three sample tourist profiles:

Budget Heritage Traveller

Mid-Budget Adventure Seeker

Family Beach Holiday

Run the agent for each profile and display the recommended itinerary.
```
## PROGRAM
```
import textwrap

destinations = [
    {"name": "Taj Mahal, Agra", "state": "Uttar Pradesh",
     "category": "heritage", "cost_per_day": 2500, "season": "Oct-Mar",
     "desc": "Iconic Mughal-era marble mausoleum, a UNESCO site."},

    {"name": "Jaipur City", "state": "Rajasthan",
     "category": "heritage", "cost_per_day": 2800, "season": "Oct-Mar",
     "desc": "The Pink City - Amber Fort, Hawa Mahal, royal palaces."},

    {"name": "Goa Beaches", "state": "Goa",
     "category": "beach", "cost_per_day": 3500, "season": "Nov-Feb",
     "desc": "Golden beaches, nightlife and water sports."},

    {"name": "Andaman Islands", "state": "Andaman & Nicobar",
     "category": "beach", "cost_per_day": 5500, "season": "Nov-Apr",
     "desc": "Pristine beaches, coral reefs, scuba diving."},

    {"name": "Manali", "state": "Himachal Pradesh",
     "category": "hill_station", "cost_per_day": 3000,
     "season": "Mar-Jun, Dec-Jan",
     "desc": "Himalayan hill town for snow and adventure sports."},

    {"name": "Ladakh", "state": "Ladakh",
     "category": "adventure", "cost_per_day": 4500,
     "season": "May-Sep",
     "desc": "High-altitude desert, monasteries, Pangong Lake."},

    {"name": "Spiti Valley", "state": "Himachal Pradesh",
     "category": "adventure", "cost_per_day": 4000,
     "season": "May-Oct",
     "desc": "Cold-desert valley for trekking and mountain biking."},

    {"name": "Coorg", "state": "Karnataka",
     "category": "adventure", "cost_per_day": 3200,
     "season": "Oct-Mar",
     "desc": "Coffee-plantation hills, trekking, waterfalls."},

    {"name": "Kerala Backwaters", "state": "Kerala",
     "category": "nature", "cost_per_day": 4000,
     "season": "Sep-Mar",
     "desc": "Houseboat cruises through backwaters and lagoons."},

    {"name": "Ranthambore National Park", "state": "Rajasthan",
     "category": "wildlife", "cost_per_day": 4800,
     "season": "Oct-Jun",
     "desc": "One of India's best parks for spotting wild tigers."},

    {"name": "Varanasi", "state": "Uttar Pradesh",
     "category": "spiritual", "cost_per_day": 2000,
     "season": "Oct-Mar",
     "desc": "Ancient city on the Ganges with temples and ghats."},

    {"name": "Rishikesh", "state": "Uttarakhand",
     "category": "spiritual", "cost_per_day": 2200,
     "season": "Sep-Nov, Feb-Apr",
     "desc": "Yoga, temples, Ganga and adventure activities."}
]


def perceive(profile):
    print(f"Tourist Profile: {profile['name']}")
    print(f"Interest       : {profile['category']}")
    print(f"Trip Duration  : {profile['days']} days")
    print(f"Daily Budget   : Rs. {profile['budget_per_day']}")
    return profile

def reason(profile):
    matches = [
        d for d in destinations
        if d["category"] == profile["category"]
        and d["cost_per_day"] <= profile["budget_per_day"]
    ]

    if not matches:
        matches = [
            d for d in destinations
            if d["category"] == profile["category"]
        ]

    matches.sort(key=lambda d: d["cost_per_day"])
    return matches


def plan(profile, matches):
    if not matches:
        return [], 0

    days_left = profile["days"]
    itinerary = []
    i = 0

    while days_left > 0 and matches:
        dest = matches[i % len(matches)]
        days_here = min(3, days_left)

        if itinerary and itinerary[-1]["destination"]["name"] == dest["name"]:
            itinerary[-1]["days"] += days_here
        else:
            itinerary.append({
                "destination": dest,
                "days": days_here
            })

        days_left -= days_here
        i += 1

    total_cost = sum(
        item["days"] * item["destination"]["cost_per_day"]
        for item in itinerary
    )

    return itinerary, total_cost


def act(itinerary, total_cost, profile):
    if not itinerary:
        print("Sorry, no destinations match this profile.")
        return

    print("\nRecommended Itinerary:")
    day_counter = 1

    for item in itinerary:
        d = item["destination"]
        end_day = day_counter + item["days"] - 1

        print(f"Day {day_counter}-{end_day}: "
              f"{d['name']} ({d['state']})")
        print(textwrap.fill(f"  {d['desc']}", width=70))
        print(f"  Best Season: {d['season']}")
        print(f"  Cost per day: Rs. {d['cost_per_day']}")

        day_counter = end_day + 1

    print(f"\nTotal Estimated Trip Cost: Rs. {total_cost} "
          f"for {profile['days']} days")


def run_agent(profile):
    profile = perceive(profile)
    matches = reason(profile)
    itinerary, total_cost = plan(profile, matches)
    act(itinerary, total_cost, profile)

sample_profiles = [
    {
        "name": "Viyana (Budget Heritage Traveller)",
        "category": "heritage",
        "days": 5,
        "budget_per_day": 4000
    },
    {
        "name": "Viyaan (Mid-Budget Adventure Seeker)",
        "category": "adventure",
        "days": 8,
        "budget_per_day": 8000
    },
    {
        "name": "The Vishwanath Family (Beach Holiday)",
        "category": "beach",
        "days": 6,
        "budget_per_day": 6000
    }
]

print("AI Tourist Agent for India")
print("=" * 60)

for idx, profile in enumerate(sample_profiles, start=1):
    print(f"\nSession {idx}")
    run_agent(profile)
    print("=" * 60)
```
## OUTPUT
<img width="690" height="703" alt="Screenshot 2026-09-22 225153" src="https://github.com/user-attachments/assets/a3e1c0ec-1c97-4912-b07b-f23b7a84f3ae" />
<img width="661" height="683" alt="Screenshot 2026-09-22 225207" src="https://github.com/user-attachments/assets/d881a9ce-5fe8-4f4f-b065-aaf7e00a6b9e" />

## Conclusion
Thus, a simple goal-based AI Tourist Agent for India was successfully designed, implemented and tested using Python. The agent follows the classic Perceive → Reason → Plan → Act cycle: it perceives a tourist's goal (interest, duration and budget), reasons over a knowledge base of Indian destinations to find matching options, plans a day-wise itinerary, and acts by presenting a complete, costed trip recommendation. This experiment demonstrates the core building blocks of autonomous agents — environment knowledge, perception, reasoning/planning and action — on which more advanced AI agents (using machine learning, real-time APIs and large language models) are built.

