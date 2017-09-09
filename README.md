# Developer Application - Eduardo Quadros

## Cover Letter

Lorem ipsum...

## Questions

### Git

#### Question 01
What are the steps you need to take before you can clone this project?

After installing git, I should set my user profile:
```
git config --global user.name "Eduardo Quadros"
git congit --global user.email "quadros.ea@gmail.com"
```

Now, considering I have access to the repository or it is set as public:

```
git clone git@gitlab.com:affinibox-public/dev-candidates.git
```

Is is nice to note that remote operations can be done through **ssh**.

#### Question 2

To help maintaining a code through development, testing and production phases, a branch flow is set in place. Usually the `master` branch is reserved for production code.

```
git checkout -b "eduardo" "develop"
```

#### Question 3
