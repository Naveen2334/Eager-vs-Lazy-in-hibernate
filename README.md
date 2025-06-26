# Eager-vs-Lazy-in-hibernate

🚀 Eager vs Lazy in Hibernate — Top Interview Questions
✅ 1. What is Lazy Loading in Hibernate?
Answer:
Lazy loading means related entities are not fetched from the database until they are accessed for the first time. Hibernate creates a proxy object initially and fires the SQL query only when the getter method of the related entity is called.

✅ 2. What is Eager Loading in Hibernate?
Answer:
Eager loading means related entities are fetched immediately along with the main entity, even if they are not accessed. Hibernate loads the association as part of the initial select query.

✅ 3. What is the default Fetch Type in Hibernate?
Answer:

For @OneToMany and @ManyToMany, the default is Lazy.

For @ManyToOne and @OneToOne, the default is Eager.

✅ 4. How to change the fetch type in Hibernate?
Answer:
By using the fetch attribute in the annotation:

java
Copy
Edit
@OneToMany(fetch = FetchType.EAGER)  
private List<Comment> comments;
✅ 5. Why is FetchType.EAGER not recommended in production?
Answer:
Eager loads all associated entities whether needed or not. For example, if a Post has 1000 comments and 1000 posts are fetched, it loads 100,000 comments unnecessarily. This increases memory consumption, degrades performance, and can lead to application crashes.

✅ 6. What is LazyInitializationException?
Answer:
When an entity is lazily loaded but the Hibernate session is already closed when its getter is accessed, Hibernate cannot fetch the data and throws LazyInitializationException.

✅ 7. How do you handle LazyInitializationException?
Answer:

Use @Transactional to keep the session open.

Fetch data eagerly via JPQL with JOIN FETCH.

Use @EntityGraph in Spring Data JPA for dynamic eager fetching.

✅ 8. How does SQL differ between Lazy and Eager fetching?
Answer:

Lazy: Fires multiple queries — one for parent and separate for each child when accessed.

Eager: Fires a join query or multiple selects immediately.

✅ 9. How to perform eager loading without FetchType.EAGER in entity?
Answer:
Using JPQL:

java
Copy
Edit
@Query("SELECT p FROM Post p JOIN FETCH p.comments WHERE p.id = :id")  
Post findPostWithComments(@Param("id") Long id);
Or with Spring Data:

java
Copy
Edit
@EntityGraph(attributePaths = "comments")  
Post findById(Long id);
✅ 10. Which is better: Eager or Lazy?
Answer:
Lazy is preferred because it avoids unnecessary loading and improves performance. Eager should be used only when the related entities are always needed together.

🔥 ⭐ Bonus Question (Advanced)
✅ 11. Can Lazy loading be applied on @ManyToOne?
Answer:
Yes. Though the default for @ManyToOne is Eager, you can override it to Lazy like this:

java
Copy
Edit
@ManyToOne(fetch = FetchType.LAZY)  
private Post post;
