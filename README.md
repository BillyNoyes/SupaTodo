## NextJS 14 Server Actions and Supabase + Auth

<p align="center">
 <img src="https://imgur.com/7Rayrls.png" width="400">
</p>

In this repo is a simple implementation of a minimal todo app, used for demo purposes, Features include:

- Server Actions
- useFormState
- Optimisitc Updates
- Supabase Database
- Supabase Auth
- Auth and oAuth example (GitHub)

### Getting Started

#### Starter Code

The branch `starter` is all the code you need to follow along with the tutorial.

#### Supabase Table

```sql
create table todos (
  id bigint generated by default as identity primary key,
  user_id uuid references auth.users not null,
  task text check (char_length(task) > 3),
  is_complete boolean default false,
  inserted_at timestamp with time zone default timezone('utc'::text, now()) not null
);
alter table todos enable row level security;
create policy "Individuals can create todos." on todos for
    insert with check (auth.uid() = user_id);
create policy "Individuals can view their own todos. " on todos for
    select using ((select auth.uid()) = user_id);
create policy "Individuals can update their own todos." on todos for
    update using ((select auth.uid()) = user_id);
create policy "Individuals can delete their own todos." on todos for
    delete using ((select auth.uid()) = user_id);
```

### Learning Points

Hopefully, from this project and the video, you can learn:

- NextJS 14 Server Actions (and drawbacks)
- Supabase Auth and Database
- useFormState
- useOptimistic

## YouTube

You can follow along with me as we build this on YouTube. The commits will line up with the YouTube chapters so you can easily see what changed in each section.

[![YouTube video](https://img.youtube.com/vi/A6-56miVA_0/0.jpg)](<[https://www.youtube.com/watch?v=A6-56miVA_0](https://youtu.be/A6-56miVA_0)>)
# SupaTodo