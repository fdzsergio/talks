background-color: #2F3440
text-strong: #1BDFD7
header-strong: #1BDFD7

# [fit] **The Young Rappel**
### Futures & Promises

---

## **Hi! I'm Sergio**
### @fdzsergio

---

## **Agenda**
#### Working with asynchronous tasks
#### Deferred computations
#### Back to the Future

---

# Async is hard

---
# Request Image

```swift 
login(with: credentials) { (result: JSONResponse) in
    if case .success(let json) = result,
    let user = User(with: json) {
        fetch(avatar: user.avatarURL) { (result: DataResponse) in
            if case .success(let data) = result {
                let image = UIImage(data: data)
                self.imageView = UIImageView(image: image)
            }
        }
    }
}
```

---

# [fit] then

---

# Request Image

```swift 
login(with: credentials)
    .then(User.init)
    .then { user in
        return fetch(avatar: user.avatarURL)
    }.then { data in
        self.imageView.image = UIImage(data: data)
    }.catch { error in 
        // handle error
    }
}
```

---

# [fit] Futures & Promises
<br>
> It is the way to handle
> complex asynchronous operations
> in a simple way

---

# What the heck is a *Future*?

---

> # Future is an object that represents that you will get something in the future.

---

# Future 
<br>

```swift
let login: Promise<User> = login(with: credentials)

login.then { user in 
    self.storage.save(user)
}
```

---

# What is a *Promise*?

---

> # A promise is an object that may produce a single value some time in the future

---

# Promise

```swift
func login(with credentials: Credentials) -> Promise<User> {
    return Promise { fulfill, reject in 
        self.client.request(task: .login(credentials)) { result in 
            switch result {
                case .success(let json):
                    fulfill(User(with: json))
                case .failure(let error):
                    reject(error)
            }
        }
    }
}
```

---

# [fit] **Common Functions**
- then
- catch
- always
- when
- all

---

# **Limitations of** Futures
- Promises can only produce one value
- Can nwot encapsulate streams of values
- Only consumer driven

---

# **Back to the Future**

- Abstraction for async/sync operations
- Encapsulate a deferred computation
- Centralized error handling 
- Easily composable

---

# [fit] De**Lorean**
![inline](assets/delorean.png)

---

##  **B-Sides**

- https://promisesaplus.com
- http://khanlou.com/2016/08/promises-in-swift
- https://speakerdeck.com/javisoto/back-to-the-futures
- https://medium.com/compileswift/hydra-promises-swift-c6319f6a6209

---

> **The Future is Today.**
-- William Osler

---

# **Thank You!**

---

# Questions?
### **@fdzsergio**
