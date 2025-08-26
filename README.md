import hashlib

def hash_password(password):
    """Hashes a password using SHA-256 for secure storage."""
    return hashlib.sha256(password.encode()).hexdigest()

def create_user(username, password, users_db):
    """Creates a new user and adds them to a database dictionary."""
    if username in users_db:
        return "Error: Username already exists."
    users_db[username] = hash_password(password)
    return f"User '{username}' created successfully."

def login_user(username, password, users_db):
    """Authenticates a user by checking the hashed password."""
    if username not in users_db:
        return "Error: Username not found."
    if users_db[username] == hash_password(password):
        return "Login successful."
    else:
        return "Error: Invalid password."

# Example usage:
users = {}
print(create_user("alice", "password123", users))
print(login_user("alice", "password123", users))
print(login_user("alice", "wrong_password", users))
