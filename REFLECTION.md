# Reflection

## 1. In `LinkedList::deleteFront()`, why does it take two separate delete calls instead of one?

Two delete calls are needed because the data and the node were created separately. `delete doomed->data` frees the object created with `new int` or `new Data` in `main.cpp`. `delete doomed` frees the node created with `new Node<T>(value)` inside `addFront()`.

## 2. Why did changing `T data[CAPACITY]` to `T* data_[CAPACITY]` make a destructor necessary?

Before the change, the array directly held the objects, so C++ cleaned them up automatically. Now it only holds pointers to objects created on the heap, so we have to delete those objects ourselves. Forgetting the destructor would leak memory, but the compiler would not give an error because the code is still valid C++.

## 3. How do `search()` and `addFront()` treat their pointers differently?

Even though both functions take a `T*`, they do not use it the same way. Once `addFront()` receives a pointer, the list owns it and has to delete it later. `search()` only borrows the pointer to compare values, so it should never delete it.

## 4. What two mechanisms allowed you to switch implementations without changing `main.cpp`?

The first mechanism is the `List<T>` base class with virtual functions, which makes both implementations follow the same set of functions. The second is the `makeList()` factory function, which decides which type of list gets created. Because of those two things, `main.cpp` does not need to know whether it is using an ArrayList or LinkedList.

## 5. Pick one keyword and explain why it matters.

I chose `override` because I probably would not have thought to add it on my own. For example, if I accidentally wrote `print()` without `const`, it would not correctly match the function in `List<T>`. Using `override` makes the compiler point out that mistake.
