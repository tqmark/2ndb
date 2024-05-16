
borrowing rules: if we have an immutable reference to something, i cannot also take a mutable reference 

each value in Rust has a variable called its owner

there can only be one owner at a time
when the owner goes out of the scope, the value will be dropped 

ownership transfer: ownership can be transferred through functions or let bindings which is known as moving. Once moved the previous owner can no longer be used

borrowing Rust allows references to a value without taking ownership

there are 2 types of borrowing

Immutable references &T which allow read-only access to the value without changing it

Mutable references &mut T, which allow modifying the value. Only one mutable reference ua allow at a time to prevent data race 

Slices is a reference to a contiguous sequence within a collection, array or string, it allow safe access to a portion of the collection without ownership
