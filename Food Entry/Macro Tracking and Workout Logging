#include <cassert>
#include <iostream>
#include <stdexcept>
#include <string>
#include <vector>
#include <unordered_map>

// ----- Application Classes -----

class FoodItem {
public:
    std::string name;
    double calories;
    double protein;
    double carbs;
    double fat;

    FoodItem() = default;
    FoodItem(const std::string& n, double cal, double prot, double carb, double f)
        : name(n), calories(cal), protein(prot), carbs(carb), fat(f) {}
};

class FoodEntry {
public:
    FoodItem food;
    double weight; // in grams
    double calories;
    double protein;
    double carbs;
    double fat;

    // Constructor calculates macros based on weight (linear scaling per 100g)
    FoodEntry(const FoodItem& foodItem, double wt)
        : food(foodItem), weight(wt)
    {
        double factor = wt / 100.0;
        calories = foodItem.calories * factor;
        protein  = foodItem.protein * factor;
        carbs    = foodItem.carbs * factor;
        fat      = foodItem.fat * factor;
    }
};

class WorkoutEntry {
public:
    std::string exercise;
    int sets;
    int reps;
    double weight; // in lbs
    double volume; // total volume = sets * reps * weight

    WorkoutEntry(const std::string& ex, int s, int r, double wt)
        : exercise(ex), sets(s), reps(r), weight(wt)
    {
        volume = sets * reps * weight;
    }
};

class App {
public:
    bool loggedIn;
    std::vector<FoodEntry> foodEntries;
    std::vector<WorkoutEntry> workoutEntries;
    std::unordered_map<std::string, FoodItem> foodDatabase;

    App() : loggedIn(false) {
        // Pre-load food items (simulating a database)
        foodDatabase["Grilled Chicken Breast"] = FoodItem("Grilled Chicken Breast", 165, 31, 0, 3.6);
    }

    // Simulate user login
    bool login(const std::string& /*username*/, const std::string& /*password*/) {
        loggedIn = true;
        return loggedIn;
    }

    // For food logging: search for a food item
    FoodItem searchFood(const std::string& query) {
        if (foodDatabase.find(query) != foodDatabase.end()) {
            return foodDatabase[query];
        }
        throw std::runtime_error("Food item not found");
    }

    // Add a food entry and return the entry index
    size_t addFoodEntry(const FoodEntry& entry) {
        foodEntries.push_back(entry);
        return foodEntries.size() - 1;
    }

    // Edit a food entry's weight (updates macros)
    void editFoodEntry(size_t index, double newWeight) {
        if (index >= foodEntries.size())
            throw std::runtime_error("Invalid food entry index");
        FoodItem food = foodEntries[index].food;
        foodEntries[index] = FoodEntry(food, newWeight);
    }

    // Delete a food entry
    void deleteFoodEntry(size_t index) {
        if (index >= foodEntries.size())
            throw std::runtime_error("Invalid food entry index");
        foodEntries.erase(foodEntries.begin() + index);
    }

    // For workout logging: add a workout entry
    size_t addWorkoutEntry(const WorkoutEntry& entry) {
        workoutEntries.push_back(entry);
        return workoutEntries.size() - 1;
    }

    // Edit a workout entry (update sets and reps)
    void editWorkoutEntry(size_t index, int newSets, int newReps) {
        if (index >= workoutEntries.size())
            throw std::runtime_error("Invalid workout entry index");
        WorkoutEntry entry = workoutEntries[index];
        workoutEntries[index] = WorkoutEntry(entry.exercise, newSets, newReps, entry.weight);
    }

    // Delete a workout entry
    void deleteWorkoutEntry(size_t index) {
        if (index >= workoutEntries.size())
            throw std::runtime_error("Invalid workout entry index");
        workoutEntries.erase(workoutEntries.begin() + index);
    }
};

// ----- Test Functions -----
// These tests simulate user actions based on the assignment's test-case document.

void testFoodEntryMacroTracking() {
    App app;
    // 1. Log in to the app.
    assert(app.login("user", "password") && "User should be logged in");

    // 2. Navigate to the food logging section (implied).
    // 3. Search for "Grilled Chicken Breast" and select 100g.
    FoodItem chicken = app.searchFood("Grilled Chicken Breast");
    FoodEntry entry100(chicken, 100.0);
    size_t entryIndex = app.addFoodEntry(entry100);

    // Verify macros for 100g: 165 kcal, 31g protein, 0g carbs, 3.6g fat.
    assert(app.foodEntries[entryIndex].calories == 165.0);
    assert(app.foodEntries[entryIndex].protein == 31.0);
    assert(app.foodEntries[entryIndex].carbs == 0.0);
    assert(app.foodEntries[entryIndex].fat == 3.6);

    // 4. Check that the entry is present in the daily summary.
    assert(app.foodEntries.size() == 1);

    // 5. Edit entry to 150g and verify updated macros.
    app.editFoodEntry(entryIndex, 150.0);
    // Expected: macros multiplied by 1.5.
    assert(app.foodEntries[entryIndex].calories == 165.0 * 1.5);
    assert(app.foodEntries[entryIndex].protein == 31.0 * 1.5);
    assert(app.foodEntries[entryIndex].carbs == 0.0 * 1.5);
    assert(app.foodEntries[entryIndex].fat == 3.6 * 1.5);

    // 6. Delete entry and verify removal from summary.
    app.deleteFoodEntry(entryIndex);
    assert(app.foodEntries.empty());
}

void testWorkoutLogging() {
    App app;
    // 1. Log in to the app.
    assert(app.login("user", "password") && "User should be logged in");

    // 2. Navigate to the workout logging page (implied).
    // 3. Log a workout: "Bench Press" with 3x10 @ 225 lbs.
    WorkoutEntry workout("Bench Press", 3, 10, 225);
    size_t workoutIndex = app.addWorkoutEntry(workout);

    // Verify total volume: 3 * 10 * 225 = 6750 lbs.
    assert(app.workoutEntries[workoutIndex].volume == 6750.0);

    // 4. Confirm the workout entry appears in the summary.
    assert(app.workoutEntries.size() == 1);

    // 5. Edit entry to 4x10 @ 225 lbs and verify updated volume (4 * 10 * 225 = 9000 lbs).
    app.editWorkoutEntry(workoutIndex, 4, 10);
    assert(app.workoutEntries[workoutIndex].volume == 9000.0);

    // 6. Delete entry and confirm removal.
    app.deleteWorkoutEntry(workoutIndex);
    assert(app.workoutEntries.empty());
}

// ----- Main Function -----

int main() {
    try {
        std::cout << "Running Food Entry / Macro Tracking tests..." << std::endl;
        testFoodEntryMacroTracking();
        std::cout << "Food Entry / Macro Tracking tests passed." << std::endl;

        std::cout << "Running Workout Logging tests..." << std::endl;
        testWorkoutLogging();
        std::cout << "Workout Logging tests passed." << std::endl;

        std::cout << "All tests passed successfully." << std::endl;
    } catch (const std::exception& ex) {
        std::cerr << "Test failed with exception: " << ex.what() << std::endl;
        return 1;
    } catch (...) {
        std::cerr << "Test failed with an unknown exception." << std::endl;
        return 1;
    }

    return 0;
}
