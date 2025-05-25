## What is PostgreSQL?

PostgreSQL হলো একটি রিলেশনাল ডাটাবেস ম্যানেজমেন্ট সিস্টেম RDBMS যা SQL ব্যবহার করে ডাটাবেস ম্যানেজ করে।
এটি ACID (Atomicity, Consistency, Isolation, Durability) বৈশিষ্ট্যসমূহ মেনে চলে যার ফলে এটি নির্ভরযোগ্য এবং ডেটা নিরাপদ রাখতে সক্ষম।

## What is the purpose of a database schema in PostgreSQL?

PostgreSQL-এ একটি ডেটাবেস স্কিমা হলো ডেটাবেসের মধ্যে অবজেক্টগুলোর  একটি সংগঠিত সংগ্রহ। 
এটি মূলত ডেটাকে বিভিন্ন ক্যাটাগরিতে সাজিয়ে রাখার একটি পদ্ধতি যাতে ডেটাবেস আরও সুসংগঠিত নিরাপদ এবং ব্যবস্থাপনা সহজ হয়।

## Explain the Primary Key and Foreign Key concepts in PostgreSQL.

Primary Key হলো একটি টেবিলের এমন একটি কলাম বা কলামের সংমিশ্রন, যা প্রতিটি রেকর্ডের জন্য অনন্য unique হতে হবে। 
এটি টেবিলের মধ্যে কোন ডুপ্লিকেট বা নাল NULL মান থাকতে দেয় না এবং প্রতিটি রেকর্ডকে সুনিদির্ষ্ট ভাবে চিহ্নিত করে।
CREATE TABLE students (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
);


Foreign Key হলো একটি কলাম বা কলামগুলির সংমিশ্রণ যা অন্য একটি টেবিলের Primary Key  এর সাথে সম্পর্কিত থাকে। 
এটি ডেটাবেসের দুইটি টেবিলের মধ্যে সম্পর্ক নির্ধারণ করে।
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name VARCHAR(50),
);

CREATE TABLE enrollments (
    enrollment_id SERIAL PRIMARY KEY,
    student_id INT,
    FOREIGN KEY (student_id) REFERENCES students(student_id)
);


## What is the difference between the VARCHAR and CHAR data types?

VARCHAR : যতটুকু অক্ষর ইনপুট দেওয়া হয় ততটুকু জায়গা ব্যবহার করে। অতিরিক্ত স্পেস হয় না।
name VARCHAR(20)
এখানে ২০ অক্ষরের মধ্যে যেকোনো দৈর্ঘ্যের নাম রাখা যাবে। যদি  “Soroar” লিখি তাহলে শুধুমাত্র 6 অক্ষর সংরক্ষিত হবে।


CHAR : নির্দিষ্ট দৈর্ঘ্যের কম হলে বাকি জায়গা স্পেস দ্বারা পুর্ন হয়। তুলনামূলক ভাবে একটু বেশি স্টোরেজ নেয়।
name CHAR(10)
এখানে যদি আপনি “Soroar” লিখি তাহলে “Soroar     ” এইভাবে 10 অক্ষরের জায়গা পুরন হবে।


## Explain the purpose of the WHERE clause in a SELECT statement.

WHERE ক্লজ SQL কুয়েরিতে ডেটা ফিল্টার করতে ব্যবহৃত হয়। এটি বিশেষ শর্তের অধীনে ডেটা নির্বাচন করার জন্য ব্যবহৃত হয়।
WHERE ক্লজের মাধ্যমে আপনি ডেটাবেসের টেবিল থেকে নির্দিষ্ট শর্তের উপর ভিত্তি করে রেকর্ড নির্বাচন করতে পারেন।
WHERE ক্লজ হল SQL এর এমন একটি টুল যা দিয়ে আপনি বলতে পারেন — আমি কেবল এই শর্ত পুরন করে এমন রেকর্ডগুলো দেখতে চাই।

SELECT * FROM students
WHERE age > 18

এখানে students টেবিল থেকে কেবল তারই তথ্য বের হবে যাদের বয়স ১৮ বছরের বেশি।


## What are the LIMIT and OFFSET clauses used for?

LIMIT এবং OFFSET  সাধারণত pagination বা বড় টেবিল থেকে নির্দিষ্ট সংখ্যক রো নির্বাচন করার জন্য ব্যবহৃত হয়।

LIMIT ক্লজ ব্যবহার করে নির্ধারণ করা যায় — কতটি রো রিটার্ন করা হবে।
SELECT * FROM products
LIMIT 5;
এটি products টেবিল থেকে মাত্র প্রথম ৫টি রো রিটার্ন করবে।


OFFSET ক্লজ ব্যবহার করে বলা যায় — কতটি রেকর্ড এড়িয়ে তারপর থেকে শুরু করতে হবে।
SELECT * FROM products
OFFSET 10;
এটি প্রথম ১০টি রো বাদ দিয়ে ১১তম রো থেকে শুরু করে সব রেকর্ড রিটার্ন করবে।


## How can you modify data using UPDATE statements?

UPDATE হলো SQL এর একটি কমান্ড যা ব্যবহার করে টেবিলের বিদ্যমান ডেটা পরিবর্তন বা সংশোধন করা হয়। 
এটি নির্দিষ্ট শর্ত অনুযায়ী একটি বা একাধিক রেকর্ডে পরিবর্তন আনতে ব্যবহৃত হয়।

UPDATE table_name
SET column1 = value1
WHERE condition;

UPDATE  কোন টেবিলে পরিবর্তন আনবেন তা নির্ধারণ করে
SET  কোন কোন কলামের মান পরিবর্তন করবেন তা বলে
WHERE  কোন রোগুলো পরিবর্তন করতে চান তা নির্ধারণ করে

UPDATE students
SET age = 21
WHERE student_id = 101;
এখানে student_id ১০১ যেই ছাত্র তার বয়স ২১ সেট করে দেওয়া হয়েছে।


## What is the significance of the JOIN operation, and how does it work in PostgreSQL?

JOIN সম্পর্কযুক্ত টেবিলগুলোর মধ্যে সংযোগ স্থাপন করে।
বিভিন্ন টেবিলের তথ্য একত্রে বিশ্লেষণ ও রিপোর্ট তৈরি করা যায়।
JOIN মূলত দুইটি বা ততোধিক টেবিলের মধ্যে একটি matching column এর ভিত্তিতে সম্পর্ক তৈরি করে এবং সেই সম্পর্ক অনুযায়ী ফলাফল দেখায়।

INNER JOIN	শুধুমাত্র মিল থাকা রেকর্ড দেখায়
LEFT JOIN বা LEFT OUTER JOIN	বাঁ দিকের টেবিলের সব রেকর্ড + ডান দিকের মিল থাকলে
RIGHT JOIN বা RIGHT OUTER JOIN	ডান দিকের টেবিলের সব রেকর্ড + বাঁ দিকের মিল থাকলে
FULL JOIN বা FULL OUTER JOIN	দুই টেবিলের সব রেকর্ড; মিল থাক বা না থাক
CROSS JOIN	Cartesian Product সব মেলানো কম্বিনেশন


SELECT students.name, classes.class_name
FROM students
INNER JOIN classes ON students.class_id = classes.class_id;
এটি শুধুমাত্র সেই ছাত্রদের দেখাবে যাদের class_id এবং classes টেবিলের class_id এর সাথে মিল আছে।


SELECT students.name, classes.class_name
FROM students
LEFT JOIN classes ON students.class_id = classes.class_id;
এটি সব ছাত্রের নাম দেখাবে, এমনকি যাদের class_id এর সাথে classes টেবিলে কোনো মিল নেই, তাদের class_name ফাঁকা থাকবে।


## Explain the GROUP BY clause and its role in aggregation operations.

GROUP BY ক্লজের মাধ্যমে আপনি একই ধরণের ডেটা একত্রে করে তাদের উপর গাণিতিক বিশ্লেষণ চালাতে পারেন।  
একই ধরনের ডেটাকে একত্রে গ্রুপ করে ফেলে এবং সেই গ্রুপগুলোর উপর অ্যাগ্রিগেট ফাংশন  SUM(), AVG(), COUNT(), MAX(), MIN() প্রয়োগ করতে দেয়।

SELECT column_name, aggregate_function(column_name)
FROM table_name
GROUP BY column_name;


## How can you calculate aggregate functions like COUNT(), SUM(), and AVG() in PostgreSQL?

Aggregate functions এমন কিছু SQL ফাংশন যেগুলো একটি কলামের একাধিক রেকর্ডের উপর গননা চালিয়ে একটি একক ফলাফল প্রদান করে।

SELECT COUNT(*) FROM students;
students টেবিলে মোট কতটি রেকর্ড আছে তা দেখাবে।

SELECT COUNT(email) FROM students;
শুধুমাত্র যেসব রোতে email ফাঁকা নেই সেগুলোর সংখ্যা দেখাবে।

SELECT SUM(marks) FROM students;
marks কলামের সব মান যোগফল দেখাবে।

SELECT AVG(marks) FROM students;
marks কলামের গড় মান average দেখাবে।


