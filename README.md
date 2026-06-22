# Student Grade Calculator
# Week 2 Project - Control Flow & Data Structures

GRADES = [
    (90, 'A', 'Excellent! Keep up the great work!'),
    (80, 'B', "Very Good! You're doing well."),
    (70, 'C', 'Good. Room for improvement.'),
    (60, 'D', 'Needs Improvement. Please study more.'),
    (0,  'F', 'Failed. Please seek help from teacher.'),
]

def calculate_grade(average):
    for threshold, grade, comment in GRADES:
        if average >= threshold:
            return grade, comment

def get_valid_number(prompt, min_val=0, max_val=100):
    while True:
        try:
            value = float(input(prompt))
            if min_val <= value <= max_val:
                return value
            print(f"Please enter a number between {min_val} and {max_val}")
        except ValueError:
            print("Invalid input! Please enter a number.")

def get_num_students():
    while True:
        try:
            n = int(input("Enter number of students: "))
            if n > 0:
                return n
            print("Please enter a positive number!")
        except ValueError:
            print("Invalid input! Please enter a whole number.")

def collect_student_data(num_students):
    names, marks, results = [], [], []
    for i in range(num_students):
        print(f"\n=== STUDENT {i+1} ===")
        name = input("Student name: ")
        while not name.strip():
            print("Name cannot be empty!")
            name = input("Student name: ")
        names.append(name)

        print("Enter marks (0-100):")
        subjects = [get_valid_number(s) for s in ("Math: ", "Science: ", "English: ")]
        marks.append(subjects)

        avg = sum(subjects) / len(subjects)
        grade, comment = calculate_grade(avg)
        results.append({'average': avg, 'grade': grade, 'comment': comment})

    return names, marks, results

def display_results(names, results):
    print("\n" + "=" * 50)
    print("            RESULTS SUMMARY")
    print("=" * 50)
    print(f"{'Name':<20} | {'Avg':>5} | {'Grade':^5} | Comment")
    print("-" * 60)
    for name, r in zip(names, results):
        print(f"{name:<20} | {r['average']:>5.1f} | {r['grade']:^5} | {r['comment']}")

def display_stats(names, results):
    averages = [r['average'] for r in results]
    print("\n" + "=" * 50)
    print("          CLASS STATISTICS")
    print("=" * 50)
    print(f"Total Students: {len(names)}")
    print(f"Class Average: {sum(averages)/len(averages):.1f}")
    print(f"Highest Average: {max(averages):.1f} ({names[averages.index(max(averages))]})")
    print(f"Lowest Average: {min(averages):.1f} ({names[averages.index(min(averages))]})")

def main():
    print("=" * 50)
    print("      STUDENT GRADE CALCULATOR")
    print("=" * 50)
    print()

    num_students = get_num_students()
    names, marks, results = collect_student_data(num_students)

    display_results(names, results)
    display_stats(names, results)

    print("\n" + "=" * 50)
    print("Thank you for using the Grade Calculator!")
    print("=" * 50)

if __name__ == "__main__":
    main()
