লারাভেল ব্রিজ ও npm ইন্সটল ও রান করার পরে। এবার আমরা লারাভেল এর সাথে যে ডিফল্ট মাইগ্রেশন ফাইল গুলো পেয়ে থাকি সেটার users ফাইল টিকে আমাদের প্রয়োজন মাফিক কাস্টমাইজ করে নি। 
ফাইলটিতে সাধারণত মেইন কোর্ড
```php
Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->rememberToken();
            $table->timestamps();
        });
```
এতটুকু থাকে এই কোড অংশটুকুকে আমরা আমাদের নিজের মতো কাস্টমাইজ করে নি। 
```php
Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('username')->nullable();
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->string('photo')->nullable();
            $table->string('phone')->nullable();
            $table->text('address')->nullable();
            $table->enum('role', ['admin', 'vendor', 'user'])->default('user');
            $table->enum('status', ['active', 'inactive'])->default('active');
            $table->rememberToken();
            $table->timestamps();
        });
```
## লারাভেল মাইগ্রেশন ফাইল: সহজ করে বোঝা

আপনি যে কোডটি দেখছেন, সেটি লারাভেল ফ্রেমওয়ার্কের একটি মাইগ্রেশন ফাইলের অংশ। মাইগ্রেশন ফাইলগুলো ব্যবহার করে আমরা আমাদের অ্যাপ্লিকেশনের ডাটাবেজের কাঠামো (structure) পরিবর্তন করতে পারি। অর্থাৎ, নতুন টেবিল তৈরি করা, পুরানো টেবিল মুছে ফেলা, কলাম যোগ করা, কলাম মুছে ফেলা ইত্যাদি কাজ করা যায়।

**এই কোডটি কী করছে?**

এই বিশেষ কোডটি একটি নতুন টেবিল তৈরি করছে যার নাম "users"। এই টেবিলটি আমাদের অ্যাপ্লিকেশনের ব্যবহারকারীদের তথ্য রাখতে ব্যবহৃত হবে। আসুন কোডটি ধাপে ধাপে বুঝে নেওয়া যাক:

* **Schema::create('users', function (Blueprint $table) {** : এই লাইনটি একটি নতুন টেবিল তৈরির জন্য একটি ফাংশন কল করে। টেবিলের নাম "users" এবং ফাংশনের ভিতরে আমরা টেবিলের কলামগুলো সংজ্ঞায়িত করব।
* **$table->id();** : এই লাইনটি টেবিলের একটি কলাম তৈরি করে যার নাম "id" এবং এটি একটি স্বয়ংক্রিয়ভাবে বৃদ্ধিপ্রাপ্ত পূর্ণসংখ্যা। এই কলামটি প্রতিটি রেকর্ডকে অনন্যভাবে চিহ্নিত করবে।
* **$table->string('name');** : এই লাইনটি একটি স্ট্রিং ধরনের কলাম তৈরি করে যার নাম "name"। এই কলামে ব্যবহারকারীর নাম সংরক্ষিত হবে।
* **$table->string('username')->nullable();** : এই লাইনটি একটি স্ট্রিং ধরনের কলাম তৈরি করে যার নাম "username" এবং এটি nullable। অর্থাৎ, এই কলামটি খালি থাকতে পারে।
* **$table->string('email')->unique();** : এই লাইনটি একটি স্ট্রিং ধরনের কলাম তৈরি করে যার নাম "email" এবং এটি unique। অর্থাৎ, এই কলামে প্রতিটি ইমেইল অ্যাড্রেস একবারের বেশি ব্যবহার করা যাবে না।
* **$table->timestamp('email_verified_at')->nullable();** : এই লাইনটি একটি timestamp ধরনের কলাম তৈরি করে যার নাম "email_verified_at" এবং এটি nullable। এই কলামে ব্যবহারকারীর ইমেইল যাচাই করার সময় সংরক্ষিত হবে।
* **$table->string('password');** : এই লাইনটি একটি স্ট্রিং ধরনের কলাম তৈরি করে যার নাম "password"। এই কলামে ব্যবহারকারীর পাসওয়ার্ড হ্যাশ করে সংরক্ষিত হবে।
* **$table->string('photo')->nullable();** : এই লাইনটি একটি স্ট্রিং ধরনের কলাম তৈরি করে যার নাম "photo" এবং এটি nullable। এই কলামে ব্যবহারকারীর প্রোফাইল ছবির পথ সংরক্ষিত হবে।
* **$table->string('phone')->nullable();** : এই লাইনটি একটি স্ট্রিং ধরনের কলাম তৈরি করে যার নাম "phone" এবং এটি nullable। এই কলামে ব্যবহারকারীর ফোন নাম্বার সংরক্ষিত হবে।
* **$table->text('address')->nullable();** : এই লাইনটি একটি text ধরনের কলাম তৈরি করে যার নাম "address" এবং এটি nullable। এই কলামে ব্যবহারকারীর ঠিকানা সংরক্ষিত হবে।
* **$table->enum('role', ['admin', 'vendor', 'user'])->default('user');** : এই লাইনটি একটি enum ধরনের কলাম তৈরি করে যার নাম "role" এবং এটি 'admin', 'vendor' বা 'user' এই তিনটি মানের একটি ধারণ করতে পারে। ডিফল্ট মান হিসেবে 'user' সেট করা আছে।
* **$table->enum('status', ['active', 'inactive'])->default('active');** : এই লাইনটি একটি enum ধরনের কলাম তৈরি করে যার নাম "status" এবং এটি 'active' বা 'inactive' এই দুটি মানের একটি ধারণ করতে পারে। ডিফল্ট মান হিসেবে 'active' সেট করা আছে।
* **$table->rememberToken();** : এই লাইনটি একটি remember_token নামের কলাম তৈরি করে যা ব্যবহারকারীকে স্বয়ংক্রিয়ভাবে লগ ইন করতে সাহায্য করে।
* **$table->timestamps();** : এই লাইনটি created_at এবং updated_at নামে দুটি কলাম তৈরি করে যা যথাক্রমে একটি রেকর্ড তৈরি হওয়ার এবং আপডেট হওয়ার সময় সংরক্ষিত করে।

**সারসংক্ষেপ:**

এই কোডটি একটি "users" নামের টেবিল তৈরি করে যা ব্যবহারকারীদের সম্পর্কিত বিভিন্ন তথ্য যেমন নাম, ইমেইল, পাসওয়ার্ড, ঠিকানা ইত্যাদি সংরক্ষণ করতে ব্যবহৃত হবে।


php artisan migrate কমান্ড চালানোর পরে মাইগ্রেশন এর সকল টেবিল তৈরি হয়ে যাবে। 
------------------
এবার মাইগ্রেশন ফাইল টি তৈরি হওয়ার পরে আমি এবার এটিতে সিডিং করতে চাচ্ছি । এর জন্য আমি php artisan make:seeder UsersTableSeeder কমান্ড দিয়ে আমার প্রয়োজনিয় সিডার ফাইলটি তৈরি করে নিলাম। ফাইল টি তৈরি হলে আমি তাতে নিচের মতো কোর্ড করি।

‘‘‘php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Facades\DB;

class UsersTableSeeder extends Seeder
{
    /**
     * Run the database seeds.
     */
    public function run(): void
    {
        DB::table('users')->insert([
            // Admin
            [
                'name' => 'admin',
                'username' => 'admin',
                'email' => 'admin@admin.com',
                'password' => Hash::make('111'),
                'role' => 'admin',
                'status' => 'active',
            ],
            // Vendor
            [
                'name' => 'vendor',
                'username' => 'vendor',
                'email' => 'vendor@vendor.com',
                'password' => Hash::make('111'),
                'role' => 'vendor',
                'status' => 'active',
            ],
            // user or customer
            [
                'name' => 'user',
                'username' => 'user',
                'email' => 'user@user.com',
                'password' => Hash::make('111'),
                'role' => 'user',
                'status' => 'active',
            ],
        ]);
    }
}
```
এখন আমরা models ফোল্ডারের লারাভেল এর সাথে যে ডিফল্ট User মডেলটি থাকে সেটিকে আমাদের প্রয়োজন মতো কাস্টমাইজ করে ব্যবহার করবো।  
