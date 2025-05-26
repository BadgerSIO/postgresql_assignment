## 1. What is PostgreSQL?

PostgreSQL হলো একটি ডাটাবেজ ম্যানেজমেন্ট সিস্টেম। এটিকে রিলেশনাল ডাটাবেজ বলা হয়ে থাকে। এই সিস্টেমটিতে ডাটা সাধারণত টেবিল আকারে ভাগ করা থাকে। একটি টেবিলে ডাটার উপর ভিত্তি করে একাধিক কলাম থাকতে পারে। একটি টেবিলে রো আকারে একাধিক ডাটা থাকে। এই সিস্টেমে দুটি টেবিলের ডাটার মধ্যে সংযোগ স্থাপন করা যায় । এটির আরেকটি আকর্ষণীয় দিক হলো এটিতে ডাটার টাইপ ডিফাইন করা যায় , যার ফলে ডাটার টাইপ সিকিউরিটি নিশ্চিত করা যায় ।

## 2. What is the purpose of a database schema in PostgreSQL?

PostgreSQL এ database schema কাজ কি আর তা যদি আমরা সহজ ভাষায় বলতে চাই , এটি একটি ডাটাবেজের অভ্যন্তরে টেবিল, ভিউ, ফাংশন, টাইপ এদেরকে ক্যাটাগরির অভ্যন্তরে নিয়ে আসতে পারে। যার ফলে আমাদের ডাটাবেজ অনেকটা সাজানো এবং গোছানো হয়। তাছাড়া আমরা চাইলে schema ভেদে ডাটাবেজ ব্যবহারকারীদের access দিতে পারি। ফলে এটি আমাদের সিস্টেমটিকে আরো সিকিউর করে তোলে। নিচে কিভাবে একটি schema তৈরি করা হয় তা দেওয়া হল

<pre lang="markdown"> <code> CREATE SCHEMA finance; 
CREATE TABLE finance.transactions ( 
    id SERIAL PRIMARY KEY, 
    amount NUMERIC, 
    date DATE );
    </code> </pre>

## 3. Explain the Primary Key and Foreign Key concepts in PostgreSQL.

Primary Key হল টেবিলের মধ্যে এমন একটি কলাম যেটি প্রত্যেকটি row কে আলাদাভাবে আইডেন্টিফাই করতে পারে। টেবিলে প্রতিটি row এর প্রাইমারি কি এর ভ্যালু আলাদা আলাদা হয়। নিচের প্রাইমারি কি এর একটি উদাহরণ দেওয়া হল

<pre lang="markdown"> <code> 
CREATE TABLE rangers (
    ranger_id SERIAL PRIMARY KEY,
    name TEXT,
    region TEXT
);

    </code> </pre>

এখানে আমরা দেখতে পাই rangers_id একটি প্রাইমারি key

অন্যদিকে Foreign Key দ্বারা দুটি টেবিলের মাঝে সম্পর্ক স্থাপন করা হয়। একটি টেবিলের Foreign Key দ্বারা অন্য একটি টেবিলের প্রাইমারি কি কে ইঙ্গিত করা হয়। নিচে একটি করেন কি এর উদাহরণ দেওয়া হলো

<pre lang="markdown"> <code> 
CREATE TABLE sightings (
    sighting_id SERIAL PRIMARY KEY,
    ranger_id INT REFERENCES rangers(ranger_id),
    species_id INT,
    sighting_time TIMESTAMP,
    location TEXT
);
    </code> </pre>

## 4. What is the difference between the VARCHAR and CHAR data types?

VARCHAR এবং CHAR ডাটা টাইপের মধ্যে মূল পার্থক্য হল CHAR এর ক্ষেত্রে আমরা চাইলে ডাটা কত ক্যারেক্টার হবে তা নির্দিষ্ট ভাবে বলে দিতে পারি । নিচে একটি CHAR এর উদাহরণ দেওয়া হল

<pre lang="markdown"> <code> 
CREATE TABLE test_char (
    code CHAR(5)
);
    </code> </pre>

এখানে আমি যদি ৫ সংখ্যক ক্যারেক্টার নির্দিষ্ট করে দেই কিন্তু ডাটা insert এর ক্ষেত্রে আমি শুধু দুই ক্যারেক্টারের ডাটা ইনসার্ট করি তবে বাকি তিন ক্যারেক্টার সে space হিসেবে নিয়ে ডাটাটি সংরক্ষণ করে।
অন্যদিকে VARCHAR ক্ষেত্রে আমরা শুধুমাত্র সর্বোচ্চ কত ক্যারেক্টার এর ডাটা হবে তা নির্ধারণ করে দিই পরবর্তীতে আমরা যত ক্যারেক্টারে না কেন তা এক্সট্রা কোন স্পেস যোগ করবে না।
নিচে একটি VARCHAR উদাহরণ দেওয়া হল

<pre lang="markdown"> <code> 
CREATE TABLE test_varchar (
    name VARCHAR(50)
);
    </code> </pre>

## 5. Explain the purpose of the WHERE clause in a SELECT statement.

WHERE ক্লজ ব্যবহার করা হয় SELECT স্টেটমেন্টে নির্দিষ্ট শর্ত অনুযায়ী ডেটা ফিল্টার করার জন্য। এটি শুধুমাত্র সেই রেকর্ডগুলো ফিরিয়ে দেয় যেগুলো শর্ত পূরণ করে।
উদাহরণ:

<pre lang="markdown"> <code> 
SELECT * FROM users WHERE age > 18;
    </code> </pre>

এখানে শুধু ১৮ বছরের বেশি বয়সী ব্যবহারকারীদের তথ্য দেখাবে।
