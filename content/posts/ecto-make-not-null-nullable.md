---
title: "Ecto make not null column nullable"
tags: ["Development", "elixir", "ecto"]
categories: ["Development", "Elixir", "Ecto"]
date: 2019-08-16T19:49:03+02:00
draft: false
---

Making a column nullable when it was not null is not obvious with Ecto however it's pretty simple.

Let's say your first migration was the following :

```ex
defmodule Foo.Repo.Migrations.CreateEvents do
  use Ecto.Migration

  def change do
    create table(:events) do
      add(:title, :string, null: false) # Title column cannot be null
    end
  end
end
```

At some point you want the title to be nullable then you should use the ecto's [modify/3](https://hexdocs.pm/ecto_sql/Ecto.Migration.html#modify/3) function.

```ex
defmodule Foo.Repo.Migrations.MakeEventTitleNullable do
  use Ecto.Migration

  def change do
    alter table(:events) do
      modify(:title, :string, null: true, from: :string) # Title column is now nullable
    end
  end
end
```
