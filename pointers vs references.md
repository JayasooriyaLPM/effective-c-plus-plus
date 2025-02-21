### **Pointers vs References in C++**  

Both **pointers** and **references** allow you to access other objects indirectly, but they behave differently.  

---

### **Key Differences**  

| Feature        | Pointers | References |
|---------------|---------|------------|
| **Can be null?** | Yes, a pointer can be set to `nullptr` (or `NULL` in older C++) | No, a reference must always refer to an actual object |
| **Can be reassigned?** | Yes, a pointer can be changed to point to another object | No, a reference is fixed to the object it was initialized with |
| **Syntax** | Uses `*` to declare and `->` to access members | Uses `&` to declare and `.` to access members |
| **Initialization** | Can be uninitialized | Must be initialized at declaration |
| **Memory Address Handling** | Stores an actual memory address | Acts as an alias (alternative name) for the object |

---

### **When to Use What?**  

#### **Use a Pointer When:**
✅ The variable might not always point to an object (i.e., it can be null).  
✅ You need to change what the variable refers to at runtime.  

**Example:**  
```cpp
int a = 10, b = 20;
int *p = &a; // Pointer points to 'a'
p = &b; // Now it points to 'b'
```

---

#### **Use a Reference When:**
✅ The variable must always refer to an object.  
✅ You don’t want to change what it refers to after initialization.  

**Example:**  
```cpp
int a = 10, b = 20;
int &r = a; // Reference to 'a'
r = b; // Changes 'a' to 20, but 'r' still refers to 'a'
```

---

### **Code Examples to Illustrate the Difference**  

#### **1. Nullability**
```cpp
int *p = nullptr; // This is allowed
int &r = *p; // ERROR! A reference cannot be null
```
🚨 A reference must always point to an existing object, while a pointer can be null.

---

#### **2. Changing What They Refer To**
```cpp
int x = 5, y = 10;

int *ptr = &x; // Pointer to x
ptr = &y; // Pointer now points to y

int &ref = x; // Reference to x
ref = y; // This does NOT make ref refer to y, it only changes x to 10
```
🚀 **Pointers can be reassigned, but references stay fixed!**  

---

#### **3. Function Parameters**
✅ **Use references for efficiency and when an object must exist.**  
✅ **Use pointers if the argument might be null.**  

**Using a Reference:**
```cpp
void printNumber(const int &num) {
    std::cout << num;
}

int x = 5;
printNumber(x); // Works fine
printNumber(nullptr); // ERROR! References cannot be null
```

**Using a Pointer:**
```cpp
void printNumber(const int *num) {
    if (num) { // Check for null
        std::cout << *num;
    }
}

int x = 5;
printNumber(&x); // Works fine
printNumber(nullptr); // Safe, since we check for null
```

🚀 **References are easier to use when you know the object always exists. Pointers are safer when nullability is a possibility.**  

---

### **Final Thoughts**
- **Use references** when you always have an object and don’t need to change what you're referring to.  
- **Use pointers** when an object may not exist or needs to be changed dynamically.  
- **References are generally safer** and preferred unless you need pointer-like behavior.  
