---
layout: post
title: "Rails: ActiveRecord::Schema"
comments: true
description: "ActiveRecord::Schema"
keywords: "activerecord"
---

## 레퍼런스 
- [ActiveRecord::Schema API](http://api.rubyonrails.org/classes/ActiveRecord/Schema.html)

## 사용법 

```
ActiveRecord::Schema.define do
  create_table :authors do |t|
    t.string :name, null: false
  end

  add_index :authors, :name, :unique

  create_table :posts do |t|
    t.integer :author_id, null: false
    t.string :subject
    t.text :body
    t.boolean :private, default: false
  end

  add_index :posts, :author_id
end
```

## define 메소드 
- 블록안의 표현식을 사용하여 DB 스키마를 정의 함 
- 표현식 안에 create_table, add_index 등의 SchemaStatements를 사용할 수 있다. 

## ActiveRecord::ConnectionAdapters::SchemaStatements 메소드 
- create_table 
```
# create_table() passes a TableDefinition object to the block.
# This form will not only create the table, but also columns for the
# table.

create_table(:suppliers) do |t|
  t.column :name, :string, limit: 60
  # Other fields here
end
```
```
# You can also use the column types as method calls, rather than calling the column method.
create_table(:suppliers) do |t|
  t.string :name, limit: 60
  # Other fields here
end
```
- :force & :cascade 
  - 테이블 생성 시 존재하면, 삭제하고 생성함 
  - 의존성이 있는 테이블에도 함께 적용 


- add_index

```
Creating a simple index
add_index(:suppliers, :name)
generates:

CREATE INDEX suppliers_name_index ON suppliers(name)
Creating a unique index
add_index(:accounts, [:branch_id, :party_id], unique: true)
generates:

CREATE UNIQUE INDEX accounts_branch_id_party_id_index ON accounts(branch_id, party_id)
Creating a named index
add_index(:accounts, [:branch_id, :party_id], unique: true, name: 'by_branch_party')
generates:

CREATE UNIQUE INDEX by_branch_party ON accounts(branch_id, party_id)
Creating an index with specific key length
add_index(:accounts, :name, name: 'by_name', length: 10)
generates:

CREATE INDEX by_name ON accounts(name(10))
Creating an index with specific key lengths for multiple keys
add_index(:accounts, [:name, :surname], name: 'by_name_surname', length: {name: 10, surname: 15})
generates:

CREATE INDEX by_name_surname ON accounts(name(10), surname(15))
Note: SQLite doesn't support index length.

Creating an index with a sort order (desc or asc, asc is the default)
add_index(:accounts, [:branch_id, :party_id, :surname], order: {branch_id: :desc, party_id: :asc})
generates:

CREATE INDEX by_branch_desc_party ON accounts(branch_id DESC, party_id ASC, surname)
Note: MySQL doesn't yet support index order (it accepts the syntax but ignores it).

Creating a partial index
add_index(:accounts, [:branch_id, :party_id], unique: true, where: "active")
generates:

CREATE UNIQUE INDEX index_accounts_on_branch_id_and_party_id ON accounts(branch_id, party_id) WHERE active
Note: Partial indexes are only supported for PostgreSQL and SQLite 3.8.0+.

Creating an index with a specific method
add_index(:developers, :name, using: 'btree')
generates:

CREATE INDEX index_developers_on_name ON developers USING btree (name) -- PostgreSQL
CREATE INDEX index_developers_on_name USING btree ON developers (name) -- MySQL
Note: only supported by PostgreSQL and MySQL

Creating an index with a specific type
add_index(:developers, :name, type: :fulltext)
generates:

CREATE FULLTEXT INDEX index_developers_on_name ON developers (name) -- MySQL
```

