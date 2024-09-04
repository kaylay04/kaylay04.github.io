---
layout: project
type: project
image: img/ArmyBuilding.jpg
title: "Army Building"
date: 2024
published: true
labels:
  - Divide and Conquer
  - Algorithms
  - Python
summary: "Chooses a optimal army using the divide and conquer algorithm."
---
Choosing an Optimal Army Using Divide and Conquer

Explanation: Divide and conquer would be a good algorithm for choosing an optimal army configuration from codices with a points budget because of its ability to manage complexity effectively while optimizing unit selection. By dividing the problem into smaller subsets based on unit attributes and combat roles, such as speed, armor, and damage capabilities, this approach allows for independent optimization within each subset. Having this division ensures that the chosen units are thoroughly evaluated for their effectiveness. Additionally, divide and conquer scales well with increasing numbers of codices and units. 

Data Structure: Using lists for storing units in a divide and conquer approach is good for its simplicity, easy manipulation, and efficient indexing, which is essential for splitting the units into subproblems. Lists maintain order, help in recursive division, and provide a O(1) time complexity for accessing elements. Recursive splitting is central to the divide and conquer approach, as it breaks down the problem into manageable chunks and combines solutions efficiently to respect the point budget while maximizing effectiveness. 

Proof of Effectiveness: The divide and conquer algorithm ensures that all possible combinations of units are considered within the points constraint by recursively breaking down the problem into smaller subproblems. This method systematically looks at all the subsets of units and assesses their total point costs and effectiveness, which take a long time to handle in large data sets. By dividing the unit list into smaller sections, the algorithm can efficiently manage and evaluate each subset, ensuring that no potential combination is overlooked. The merging function helps this process by combining the optimal solutions from these subproblems. It evaluates the combined point costs and effectiveness of every possible pair of left and right solutions, ensuring that the best possible combination of units is selected. Therefore, the merging function guarantees that the final selected combination is the most effective one, balancing both the points constraint and the overall combat capability of the units.

""" 
Justine Afaga
Alexis Karl Buted
Kayla Young 
"""


"The `Unit` class constructor initializes an object with attributes representing a unit's name, speed, wounds, armor, shooting accuracy, shooting damage, close combat accuracy, close combat damage, and point cost. Each attribute is assigned a value based on the parameters provided when creating a new `Unit` instance."
class Unit:
    def __init__(self, name, speed, wounds, armor, shooting_accuracy, shooting_damage, close_combat_accuracy, close_combat_damage, point_cost):
        self.name = name
        self.speed = speed
        self.wounds = wounds
        self.armor = armor
        self.shooting_accuracy = shooting_accuracy
        self.shooting_damage = shooting_damage
        self.close_combat_accuracy = close_combat_accuracy
        self.close_combat_damage = close_combat_damage
        self.point_cost = point_cost

"This code creates a list of `Unit` objects, each initialized with specific attributes such as name, speed, wounds, armor, shooting accuracy, shooting damage, close combat accuracy, close combat damage, and point cost. Each `Unit` instance in the list represents a unique unit with distinct characteristics used for later calculations and simulations."
units = [
    Unit("Unit1", 5, 10, 0.8, 0.9, 20, 0.7, 15, 100),
    Unit("Unit2", 6, 8, 0.7, 0.85, 18, 0.75, 12, 80),
    Unit("Unit3", 4, 12, 0.75, 0.8, 22, 0.6, 18, 120),
    Unit("Unit4", 7, 7, 0.65, 0.9, 19, 0.8, 14, 70),
    Unit("Unit5", 3, 15, 0.85, 0.78, 25, 0.5, 20, 150),
    Unit("Unit6", 8, 6, 0.6, 0.92, 17, 0.85, 13, 60),
    Unit("Unit7", 5, 9, 0.7, 0.88, 20, 0.75, 16, 90),
    Unit("Unit8", 4, 11, 0.8, 0.83, 21, 0.65, 17, 110),
    Unit("Unit9", 6, 10, 0.9, 0.86, 18, 0.78, 14, 95),
    Unit("Unit10", 7, 8, 0.65, 0.87, 16, 0.8, 15, 85),
]

"The `calculate_effectiveness` function computes the effectiveness of a unit by multiplying its number of wounds by its shooting damage and then adding its close combat damage. This gives a single numerical value representing the unit's overall combat capability."
def calculate_effectiveness(unit):
    return unit.wounds * unit.shooting_damage + unit.close_combat_damage

"The function `calculate_effectiveness(unit)` computes the combat effectiveness of a unit based on its wounds, shooting damage, and close combat damage. The `Combat(unitA, unitB, distance)` function compares two units (`unitA` and `unitB`) based on their calculated shooting or close combat effectiveness, depending on the specified distance, and returns the unit with higher effectiveness in simulated combat."
def Combat(unitA, unitB, distance):
    if distance > 5:
        # At long range, shooting matters more
        shooting_effectiveness_A = unitA.shooting_accuracy * unitA.shooting_damage
        shooting_effectiveness_B = unitB.shooting_accuracy * unitB.shooting_damage
    else:
        # Up close, close combat matters more
        shooting_effectiveness_A = unitA.close_combat_accuracy * unitA.close_combat_damage
        shooting_effectiveness_B = unitB.close_combat_accuracy * unitB.close_combat_damage
    
    total_effectiveness_A = shooting_effectiveness_A * unitA.wounds
    total_effectiveness_B = shooting_effectiveness_B * unitB.wounds
    
    return unitA if total_effectiveness_A > total_effectiveness_B else unitB

"The `Battle` function simulates a battle between two armies (`armyA` and `armyB`) based on the cumulative effectiveness of their respective units. It sums up the effectiveness of each unit in both armies using the `calculate_effectiveness` function and then determines the outcome based on which army has a higher total effectiveness, returning 'Army A wins' if `effectiveness_A` is greater, otherwise 'Army B wins'."
def Battle(armyA, armyB, battlefieldF):
    effectiveness_A = sum(calculate_effectiveness(unit) for unit in armyA)
    effectiveness_B = sum(calculate_effectiveness(unit) for unit in armyB)
    
    return "Army A wins" if effectiveness_A > effectiveness_B else "Army B wins"

"The `merge_solutions` function combines two sets of solutions (`left_solutions` and `right_solutions`) from a divide-and-conquer algorithm to find the best combination of armies that fit within a maximum points constraint (`max_points`). It iterates through all possible combinations of left and right solutions, calculating their combined points and effectiveness. It keeps track of the best army configuration (`best_army`) and its effectiveness (`best_effectiveness`) that meets the criteria, finally returning these optimal values."
def merge_solutions(left_solutions, right_solutions, max_points):
    best_army = []
    best_effectiveness = 0

    for l_army, l_points, l_effectiveness in left_solutions:
        for r_army, r_points, r_effectiveness in right_solutions:
            total_points = l_points + r_points
            if total_points <= max_points:
                total_effectiveness = l_effectiveness + r_effectiveness
                if total_effectiveness > best_effectiveness:
                    best_army = l_army + r_army
                    best_effectiveness = total_effectiveness

    return best_army, best_effectiveness

"The `optimal_army_divide_and_conquer` function recursively finds the best combination of units within a specified maximum points constraint (`max_points`). It returns the optimal army configuration, total points used, and its effectiveness if there's only one unit or no units that fit within the points constraint."
def optimal_army_divide_and_conquer(units, max_points):
    if not units or max_points <= 0:
        return [], 0, 0

    if len(units) == 1:
        unit = units[0]
        if unit.point_cost <= max_points:
            return [unit], unit.point_cost, calculate_effectiveness(unit)
        else:
            return [], 0, 0

    "These lines of code split the list of `units` into two halves: `left_units` containing the first half of the units up to but not including the middle (`mid`), and `right_units` containing the units from the middle (`mid`) to the end of the list. This splitting is typically used in divide-and-conquer algorithms to divide a problem into smaller subproblems for processing."
    mid = len(units) // 2
    left_units = units[:mid]
    right_units = units[mid:]

    "These lines of code demonstrate the recursive approach in the `optimal_army_divide_and_conquer` function. It divides the problem of selecting the optimal army into smaller subproblems by recursively calling itself with `left_units` and `right_units`. It then merges the solutions from these subproblems using the `merge_solutions` function to find the best combination of units within the `max_points` constraint. Finally, it returns the best army configuration (`best_army`), the total points used by that configuration, and its effectiveness."
    left_solution = [optimal_army_divide_and_conquer(left_units, max_points)]
    right_solution = [optimal_army_divide_and_conquer(right_units, max_points)]

    best_army, best_effectiveness = merge_solutions(left_solution, right_solution, max_points)

    return best_army, sum(unit.point_cost for unit in best_army), best_effectiveness

"These lines of code set `max_points` to 300, then use the `optimal_army_divide_and_conquer` function to find the best combination of units (`optimal_units`) within this points constraint from the `units` list. It also calculates `total_points` and `total_effectiveness` of the optimal army configuration. Finally, it creates `optimal_units_list`, which stores tuples containing the name, point cost, and effectiveness of each unit in the optimal army."
max_points = 300

optimal_units, total_points, total_effectiveness = optimal_army_divide_and_conquer(units, max_points)

optimal_units_list = [(unit.name, unit.point_cost, calculate_effectiveness(unit)) for unit in optimal_units]

"The provided code snippet first prints detailed information about the units in the optimal army configuration, including their names, costs, and effectiveness. It then simulates combat between two specific units and a battle between predefined armies, displaying the outcomes of these simulated scenarios."
print("Optimal Army:")
for unit in optimal_units:
    print(f"{unit.name} - Cost: {unit.point_cost}, Effectiveness: {calculate_effectiveness(unit)}")
print(f"Total Effectiveness: {total_effectiveness}")

print("\nCombat:")
winner = Combat(units[0], units[1], 10)
print(f"Winner: {winner.name}")

print("\nBattle:")
armyA = [units[0], units[1], units[2]]
armyB = [units[3], units[4]]
result = Battle(armyA, armyB, "Field")
print(result)

