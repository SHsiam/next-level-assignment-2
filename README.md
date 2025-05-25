১. What is PostgreSQL?

PostgreSQL একটি শক্তিশালী, ওপেন সোর্স রিলেশনাল ডেটাবেইস ম্যানেজমেন্ট সিস্টেম। এটি SQL এবং JSON উভয়কেই সমর্থন করে। PostgreSQL কে "Postgres" নামেও ডাকা হয়।
এটি বড় আকারের অ্যাপ্লিকেশন যেমন ওয়েব অ্যাপ, এনালিটিকাল টুলস, বা মোবাইল অ্যাপ ব্যাকএন্ডে ব্যবহৃত হয় কারণ এতে রয়েছে জটিল কুয়েরি সাপোর্ট, ইন্ডেক্সিং, পার্শিয়াল ফিচার, এবং ইউজার-ডিফাইন্ড ফাংশনস ইত্যাদি।

2. What is the purpose of a database schema in PostgreSQL?

Schema হলো ডেটাবেসের মধ্যে একটি লজিক্যাল কাঠামো। এটি বিভিন্ন টেবিল, ভিউ, ফাংশন, এবং অন্যান্য অবজেক্টকে একটি নামকৃত গ্রুপে সংগঠিত করে।
এর মাধ্যমে একই ডেটাবেসের মধ্যে একাধিক Schema রাখতে পারে যাতে name conflict এড়ানো যায়।
Example: SELECT * FROM sales.customers;
SELECT * FROM hr.customers;

৩. Explain the Primary Key and Foreign Key concepts in PostgreSQL.

Primary Key এমন একটি কলাম যা প্রতিটি রেকর্ডকে ইউনিকভাবে সনাক্ত করে। এটি NULL হতে পারে না।
Foreign Key হলো একটি টেবিলের একটি কলাম যা অন্য টেবিলের Primary Key-এর দিকে রেফারেন্স করে। এটি দুই টেবিলের মধ্যে সম্পর্ক তৈরি করে।
Example: CREATE TABLE departments (
  dept_id SERIAL PRIMARY KEY,
  dept_name TEXT NOT NULL
);

CREATE TABLE employees (
  emp_id SERIAL PRIMARY KEY,
  emp_name TEXT NOT NULL,
  dept_id INTEGER REFERENCES departments(dept_id)
);

৪. What is the difference between the VARCHAR and CHAR data types?

VARCHAR এবং CHAR উভয়ই string টাইপ ডেটা সংরক্ষণের জন্য ব্যবহৃত হয়, তবে মূল পার্থক্য হলো:

CHAR: নির্দিষ্ট দৈর্ঘ্যের ফিক্সড সাইজ string। কম অক্ষরের string সেভ করে, এটা টেবিলে 'Ram ' স্পেস সহ সংরক্ষিত হবে।

VARCHAR: পরিবর্তনশীল দৈর্ঘ্যের string, যা সর্বাধিক n অক্ষর পর্যন্ত যেতে পারে, এবং অতিরিক্ত স্পেস ব্যবহার করে না।

৫. Explain the purpose of the WHERE clause in a SELECT statement.

WHERE ক্লজ একটি ফিল্টার হিসেবে কাজ করে। এটি SELECT স্টেটমেন্টে ব্যবহৃত হয় যাতে নির্দিষ্ট শর্ত পূরণ করে রেকর্ডগুলোই ফেরত দেওয়া হয়।
Example: SELECT * FROM employees WHERE dept_id = 2;

৬. What are the LIMIT and OFFSET clauses used for?

LIMIT ও OFFSET ক্লজ ব্যবহার করে ডেটার নির্দিষ্ট অংশ রিটার্ন করাতে পারে। Pagination-এর জন্য এটি খুবই উপযোগী।
LIMIT কুয়েরি থেকে সর্বোচ্চ n সংখ্যক রেকর্ড ফেরত দেয়।
OFFSET m সংখ্যক রেকর্ড বাদ দিয়ে পরবর্তী রেকর্ড থেকে শুরু করে রেজাল্ট রিটার্ন করে।
Example: SELECT * FROM employees LIMIT 5 OFFSET 10;

৭. What is the significance of the JOIN operation, and how does it work in PostgreSQL?

JOIN অপারেশন দুটি বা ততোধিক টেবিলের মধ্যে সম্পর্ক তৈরি করে এবং ডেটা সংযুক্ত করে। এটি ডেটাবেইস নরমালাইজেশনের মূল ভিত্তি।
Types of Join:
1. INNER JOIN
2. LEFT JOIN
3. RIGHT JOIN
4. FULL OUTER JOIN
Example: SELECT e.emp_name, d.dept_name
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id;

৮. How can you calculate aggregate functions like COUNT(), SUM(), and AVG() in PostgreSQL?

এই ফাংশনগুলো ডেটার উপর গাণিতিক বিশ্লেষণ চালায়:
COUNT(): রেকর্ডের সংখ্যা গণনা করে।
SUM(): নির্দিষ্ট কলামের মোট যোগফল বের করে।
AVG(): নির্দিষ্ট কলামের গড় মান গণনা করে।
Example: SELECT COUNT(*) FROM employees;
SELECT SUM(salary) FROM employees WHERE dept_id = 1;
SELECT AVG(salary) FROM employees;


