---
layout: post
title:  "Django Intro"
categories: django, migration, models
---

## Basics
* Create an admin user `python manage.py createsuperuser`
* Run the server `python manage.py runserver`
* __Views__: public interface
* __A URL pattern__ is simply the general form of a URL - for example: `/newsarchive/<year>/<month>/`. A __URLconf__ maps URL patterns to views.
* The __render()__ function takes the request object as its first argument, a template name as its second argument and a dictionary as its optional third argument. It returns an __HttpResponse__ object of the given template rendered with the given context
* The __get_object_or_404()__ function takes a Django model as its first argument and an arbitrary number of keyword arguments, which it passes to the __get()__ function of the model's manager. It raises __Http404__ if the object doesn't exist. Similarly there is __get_list_or_404()__.
* Whenever you create a form that alters data server-side, use __method="post"__.
* All POST forms that are targeted at internal URLs should use the __csrf_token__ liquid template tag.
* Per-object summaries can be generated using the __annotate()__ clause. When an __annotate()__ clause is specified, each object in the __QuerySet__ will be annotated with the specified values. [django doc on annotate](https://docs.djangoproject.com/en/2.0/topics/db/aggregation/#generating-aggregates-for-each-item-in-a-queryset)
* __django.contrib.staticfiles__: collects static files from each of your applications (and any other places you specify) into a single location that can easily be served in production.


## Django Migrations

### Three-step guide to making model changes:

* Change your models (in _models.py_).
* Run `python manage.py makemigrations` to create migrations for those changes
* Run `python manage.py migrate` to apply those changes to the database.

### Breakdown

* By running `makemigrations`, you're telling Django that you've made some changes to your models and that you'd like the changes to be stored as a migration.

```bash
jj@viserion:src $ python manage.py makemigrations polls
Migrations for 'polls':
  polls/migrations/0001_initial.py
    - Create model Choice
    - Create model Question
    - Add field question to choice
```


* The `sqlmigrate` command takes migration names and returns their SQL.
It doesn't actually run the migration on your database - it just prints it to the screen so that you can see what SQL Django thinks is required. It's useful for checking what Django is going to do or if you have database administrators who require SQL scripts for changes.

```bash
jj@viserion:src $ python manage.py sqlmigrate polls 0001
BEGIN;
--
-- Create model Choice
--
CREATE TABLE "polls_choice" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "choice_text" varchar(200) NOT NULL, "votes" integer NOT NULL);                                              
--
-- Create model Question
--
CREATE TABLE "polls_question" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "question_text" varchar(200) NOT NULL, "pub_date" datetime NOT NULL);                                      
--
-- Add field question to choice
--
ALTER TABLE "polls_choice" RENAME TO "polls_choice__old";
CREATE TABLE "polls_choice" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "choice_text" varchar(200) NOT NULL, "votes" integer NOT NULL, "question_id" integer NOT NULL REFERENCES "polls_question" ("id") DEFERRABLE INITIALLY DEFERRED);
INSERT INTO "polls_choice" ("id", "choice_text", "votes", "question_id") SELECT "id", "choice_text", "votes", NULL FROM "polls_choice__old";                                               
DROP TABLE "polls_choice__old";
CREATE INDEX "polls_choice_question_id_c5b4b260" ON "polls_choice" ("question_id");
COMMIT;
```

* The `migrate` command takes all the migrations that haven't been applied (Django tracks which ones are applied using a special table in your database called django_migrations) and runs them against your database - essentially, synchronizing the changes you made to your models with the schema in the database.
