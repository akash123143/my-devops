
List of all conditional statements 

1. If statement : 
2. case statement
3. while loop 
4. until loop 
5. For loop
6. test command
# Explanation

#### If statement 
Executes commands based on a condition.
```
if [ condition ]; then
    # commands
elif [ another_condition ]; then
    # commands
else
    # commands
fi

```
#### Case statement 
Used for multiple conditions, similar to a switch-case in other languages.
```
case variable in
    pattern1)
        # commands
        ;;
    pattern2)
        # commands
        ;;
    *)
        # commands if no pattern matches
        ;;
esac

```
#### While loop
Repeats commands as long as a condition is true.
```
while [ condition ]; do
    # commands
done

```
#### Until loop
Repeats commands until a condition becomes true.
```
until [ condition ]; do
    # commands
done

```
#### For loop
Iterates over a list or a range of values.
```
for variable in list; do
    # commands
done

```
#### Test command
To evaluate the condition and run commands based on the Boolean state.
```
test condition && commands_if_true
test condition || commands_if_false

```
