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
