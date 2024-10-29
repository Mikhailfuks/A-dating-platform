class User {
    constructor(username, age, gender, interests) {
        this.username = username;
        this.age = age;
        this.gender = gender;
        this.interests = interests;
    }
}

class DatingPlatform {
    constructor() {
        this.users = [];
    }

    registerUser(username, age, gender, interests) {
        const newUser = new User(username, age, gender, interests);
        this.users.push(newUser);
        console.log(`User registered: ${username}`);
    }

    findMatches(user) {
        const matches = this.users.filter(otherUser => {
            return otherUser.username !== user.username &&
                   otherUser.gender !== user.gender && // Assuming straight relationships
                   this.hasCommonInterests(user, otherUser);
        });
        return matches;
    }

    hasCommonInterests(user1, user2) {
        return user1.interests.some(interest => user2.interests.includes(interest));
    }

    listUsers() {
        return this.users.map(user => user.username);
    }
}

// Example Usage
const datingPlatform = new DatingPlatform();

// Register users
datingPlatform.registerUser('Alice', 25, 'female', ['music', 'travel', 'reading']);
datingPlatform.registerUser('Bob', 27, 'male', ['sports', 'music']);
datingPlatform.registerUser('Charlie', 22, 'male', ['movies', 'travel']);
datingPlatform.registerUser('Diana', 26, 'female', ['cooking', 'music']);

// Find matches for Alice
const alice = datingPlatform.users.find(user => user.username === 'Alice');
const matchesForAlice = datingPlatform.findMatches(alice);

// Display matches
console.log(`Matches for ${alice.username}:`, matchesForAlice.map(user => user.username));
