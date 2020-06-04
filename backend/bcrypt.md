__BCrypt__ → password hashing function. The hashes produced by it are considered very secured.

## Hash Structure
`$2a$13$ZyprE5MRw2Q3WpNOGZWGbeG7ADUre1Q8QO.uUUtcbqloU0yvzavOm`
- `$2a` → what kind of hash algorithm was used.
- `$13` → cost.
- `$ZyprE5MRw2Q3WpNOGZWGbeG7ADUre1Q8QO.uUUtcbqloU0yvzavOm` → first 22 characters is the salt in plain text, and the rest the hashed password.

## Using the `bcrypt` npm package
We need to install the `bcrypt` package in our server to use it.\
Hashing is computationally intensive, so it's recommended to do it asynchronously on your server.

_Hashing a password:_
```javascript
bcrypt.hash(<plainTextPassword>, <saltRounds>, (err, hash) => {
  // Store the hash in the DB
})
```

_Comparing hashed passwords:_
```javascript
bcrypt.compare(<plainTextPassword>, <hashedPassword>, (err, res) => {

})
```
This will return true or false depending if the passwords match or not.

_Hash the password synchronously:_
```javascript
const hash = bcrypt.hashSync(<plainTextPassword>, <saltRounds>)
```

_Compare hashed passwords synchrounously:_
```javascript
const result = bcrypt.compareSync(<plainTextPassword>, <hashesdPassword>)
```

# Keywords
__hash__ → returned fixed value of an algorithm that was fed some kind of data. They are always unique.
__salt__ → random data added to the original data before the hashing process. Makes the hash harder to crack.
__cost__ → how much power it takes to compute the hash on a logarithmic scale of 2^cost. For example, at a cost of 10 we are able to hash 10 passwords a second on an average computer, however at a cost of 15 it takes 3 seconds per hash. A cost of 12 is considered very secure at this time.