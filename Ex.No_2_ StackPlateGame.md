## <p align="center"> EX.NO : 2 -- IMPLEMENTATION OF STACK PLATE GAME USING QUEUE... </p>

#### DATE : 16.08.2024      
#### NAME : Anto Richard. S
#### REGISTER NUMBER : 212221240005

### AIM :

To write a python program to simulate the process of stacking plates.

### ALGORITHM :

### Step 1 :

Initialize the Stack.

### Step 2 :

Create an empty list to represent the stack.

### Step 3 :

Push the plate on top of stack.

### Step 4 :

Pop the plate from top.

### Step 5 :

Display the plate details.

### Step 6 :

Create an interactive menu and display it.

### PROGRAM :

```python
class PlateStack:
    def __init__(self):
        self.stack = []

    def is_empty(self):
        return len(self.stack) == 0

    def push(self, plate):
        self.stack.append(plate)
        print(f"Plate '{plate}' added to the stack.")

    def pop(self):
        if self.is_empty():
            print("The stack is empty. No plates to remove.")
        else:
            removed_plate = self.stack.pop()
            print(f"Plate '{removed_plate}' removed from the stack.")

    def view_stack(self):
        if self.is_empty():
            print("The stack is empty.")
        else:
            print("Current stack of plates:")
            for plate in reversed(self.stack):
                print(plate)
```

```python
def plate_stack_game():
    plate_stack = PlateStack()
    print("Welcome to the Plate Stack Game!")

    while True:
        print("\nChoose an option:")
        print("1. Add a plate")
        print("2. Remove a plate")
        print("3. View stack")
        print("4. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            plate = input("Enter the name of the plate to add: ")
            plate_stack.push(plate)
        elif choice == '2':
            plate_stack.pop()
        elif choice == '3':
            plate_stack.view_stack()
        elif choice == '4':
            print("Exiting the game. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")
```

```python
if __name__ == "__main__":
    plate_stack_game()
```

### OUTPUT :

![aifg-2 1](https://github.com/user-attachments/assets/9a59e106-4ea4-4708-b2a9-dff1729c9f3d)

![aifg-2 2](https://github.com/user-attachments/assets/0fa6d5bd-b137-4347-b866-97abedf0867c)

![aifg-2 3](https://github.com/user-attachments/assets/d04e9309-2bf7-413b-8b9d-4f1fcb263de5)

![aifg-2 4](https://github.com/user-attachments/assets/d02cbf68-99de-4c73-9dd3-6f027cbf50b3)

### RESULT :

Thus, the simple Stack plate game was implemented using data structure Stack.

