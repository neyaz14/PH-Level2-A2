Bonus Section: PostgreSQL প্রশ্নের উত্তর (বাংলায় বিশ্লেষণসহ)
1️⃣ PostgreSQL কী?
PostgreSQL হলো একটি অবজেক্ট-রিলেশনাল ডাটাবেইস ম্যানেজমেন্ট সিস্টেম (ORDBMS)। এটি একটি ওপেন সোর্স এবং highly extensible ডাটাবেইস সিস্টেম যা ডেভেলপারদের স্কেলযোগ্য এবং নিরাপদ অ্যাপ্লিকেশন তৈরি করতে সহায়তা করে।

এটি SQL (Structured Query Language) ব্যবহার করে ডেটা ম্যানেজ করে, কিন্তু সাধারণ RDBMS-এর তুলনায় এটি আরও বেশি ফিচার অফার করে, যেমন:

JSON এবং XML সাপোর্ট

Stored procedures

Full-text search

Custom data types

Concurrency control (MVCC)

📌 উদাহরণস্বরূপ, যদি আপনি একটি ই-কমার্স সাইট তৈরি করেন, তাহলে PostgreSQL ব্যবহার করে আপনি পণ্য, অর্ডার, ইউজার, পেমেন্ট ইত্যাদি সব ডেটা নিরাপদভাবে সংরক্ষণ ও প্রক্রিয়া করতে পারেন।

2️⃣ PostgreSQL-এ Schema-এর উদ্দেশ্য কী?
একটি schema হচ্ছে ডাটাবেইসের মধ্যে একটি লজিক্যাল স্ট্রাকচার বা নামের জায়গা (namespace), যা টেবিল, ভিউ, ফাংশন, ট্রিগার ইত্যাদি সংগঠিত করে।

➡️ উদ্দেশ্য:

বড় ডাটাবেইসে ডেটা আলাদা করে গুছিয়ে রাখা

ভিন্ন ভিন্ন ইউজারের জন্য আলাদা স্কিমা তৈরি করা যায়

একই নামের টেবিল বা অবজেক্ট একাধিক স্কিমায় রাখা যায়

📌 উদাহরণ:
একটি বিশ্ববিদ্যালয় ম্যানেজমেন্ট সিস্টেমে students, teachers, ও admin - এই তিনটি স্কিমা থাকতে পারে যাতে তাদের নিজ নিজ টেবিল থাকে।

sql
Copy
Edit
CREATE SCHEMA students;
CREATE TABLE students.info (id SERIAL PRIMARY KEY, name VARCHAR(50));
3️⃣ Primary Key এবং Foreign Key কী এবং কীভাবে কাজ করে?
✅ Primary Key:

একটি টেবিলের প্রধান ফিল্ড যা অনন্য (unique) এবং ফাঁকা (NULL) হতে পারে না।

প্রতিটি row কে অভিন্নভাবে শনাক্ত করতে ব্যবহার হয়।

sql
Copy
Edit
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100)
);
✅ Foreign Key:

একটি টেবিলের এমন একটি কলাম যা অন্য টেবিলের Primary Key-কে রেফারেন্স করে।

এটি দুই টেবিলের মধ্যে সম্পর্ক তৈরি করে এবং ডেটা ইন্টিগ্রিটি বজায় রাখে।

sql
Copy
Edit
CREATE TABLE orders (
  id SERIAL PRIMARY KEY,
  user_id INT REFERENCES users(id)
);
📌 উদাহরণ: orders.user_id হলো users.id এর foreign key।

4️⃣ VARCHAR ও CHAR-এর মধ্যে পার্থক্য কী?
Feature	VARCHAR	CHAR
Full Form	Variable Character	Character
Data Length	Dynamic (variable length)	Fixed length
Space Usage	ব্যবহার অনুযায়ী জায়গা নেয়	সব সময় নির্দিষ্ট জায়গা নেয়
Performance	Memory efficient	কম efficient
Example	VARCHAR(50) = 5 characters → 5 bytes	CHAR(50) = 5 characters → still 50 bytes

📌 সাধারণভাবে, VARCHAR বেশি ব্যবহার হয় কারণ এটি মেমোরি অপ্টিমাইজ করে।

5️⃣ SELECT স্টেটমেন্টে WHERE ক্লজ-এর উদ্দেশ্য কী?
WHERE ক্লজ ব্যবহার করে ডেটা ফিল্টার করা হয়। অর্থাৎ, আপনি যেসব রেকর্ড দেখতে চান, শুধুমাত্র সেগুলোই শর্ত (condition) অনুযায়ী নির্বাচন করা হয়।

sql
Copy
Edit
SELECT * FROM users WHERE age > 25;
📌 উপরের কোডটি কেবল তাদেরকেই দেখাবে যাদের বয়স ২৫-এর বেশি।

6️⃣ LIMIT এবং OFFSET কী কাজে লাগে?
✅ LIMIT: কতটি রেকর্ড দেখতে চান তা নির্ধারণ করে
✅ OFFSET: কতটি রেকর্ড স্কিপ করতে চান তা নির্ধারণ করে

📌 Pagination-এ ব্যবহৃত হয়।

sql
Copy
Edit
SELECT * FROM orders LIMIT 10 OFFSET 20;
👉 এটি ২১ নম্বর থেকে শুরু করে ১০টি অর্ডার দেখাবে।

7️⃣ UPDATE দিয়ে কীভাবে ডেটা পরিবর্তন করা যায়?
UPDATE স্টেটমেন্ট ব্যবহার করে টেবিলের বিদ্যমান ডেটা পরিবর্তন করা হয়।

sql
Copy
Edit
UPDATE users SET name = 'Neyaz Updated' WHERE id = 1;
⚠️ অবশ্যই WHERE ক্লজ ব্যবহার করতে হবে, না হলে পুরো টেবিল আপডেট হয়ে যাবে।

8️⃣ JOIN-এর গুরুত্ব এবং এটি কীভাবে কাজ করে?
JOIN ব্যবহার করে আমরা একাধিক টেবিলের মধ্যে সম্পর্ক তৈরি করে একসাথে ডেটা রিটার্ন করতে পারি।

✅ প্রধান JOIN টাইপগুলো:

INNER JOIN: কেবল মিল থাকা রেকর্ড রিটার্ন করে

LEFT JOIN: বাম টেবিলের সব রেকর্ড + মিল থাকলে ডান টেবিল

RIGHT JOIN: ডান টেবিলের সব রেকর্ড + মিল থাকলে বাম টেবিল

FULL JOIN: উভয় টেবিলের সব রেকর্ড

📌 উদাহরণ:

sql
Copy
Edit
SELECT users.name, orders.id
FROM users
INNER JOIN orders ON users.id = orders.user_id;
👉 এটি দেখাবে কোন ইউজার কোন অর্ডার করেছে।

9️⃣ GROUP BY-এর কাজ কী? Aggregation-এ এটি কীভাবে সাহায্য করে?
GROUP BY ক্লজ ব্যবহার করে ডেটাকে নির্দিষ্ট ক্যাটাগরিতে ভাগ করে প্রত্যেক গ্রুপে Aggregate ফাংশন প্রয়োগ করা যায়।

📌 উদাহরণ:

sql
Copy
Edit
SELECT department, COUNT(*) 
FROM students 
GROUP BY department;
👉 এটি প্রতিটি ডিপার্টমেন্টে কতজন ছাত্র আছে তা দেখাবে।

🔟 COUNT(), SUM(), AVG() কী এবং কীভাবে ব্যবহার হয়?
✅ COUNT(): মোট রেকর্ড সংখ্যা
✅ SUM(): সংখ্যার মোট যোগফল
✅ AVG(): গড় হিসাব

📌 উদাহরণ:

sql
Copy
Edit
SELECT COUNT(*) FROM orders;
SELECT SUM(amount) FROM orders WHERE status = 'paid';
SELECT AVG(age) FROM users;
👉 এগুলোর মাধ্যমে ডেটা থেকে ইনসাইট বের করা সহজ হয়, যেমন কত টাকা আয় হয়েছে, গড় বয়স কত, ইত্যাদি।