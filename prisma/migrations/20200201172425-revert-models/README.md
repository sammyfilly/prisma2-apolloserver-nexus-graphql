# Migration `20200201172425-revert-models`

This migration has been generated by hatchli at 2/1/2020, 5:24:25 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql

```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20200201172104-update-capitalization-models..20200201172425-revert-models
--- datamodel.dml
+++ datamodel.dml
@@ -3,29 +3,29 @@
 }
 datasource mysql {
   provider = "mysql"
-  url = "***"
+  url      = "mysql://prisma:F1g+sparrow@prisma.clisj67py2b1.us-east-2.rds.amazonaws.com:3306/prisma"
 }
-model Post {
+model post {
   content    String?
   created_at DateTime?
   post_id    Int       @default(autoincrement()) @id
   title      String    @default("")
-  author_id  User
+  author_id  user
 }
-model Profile {
+model profile {
   bio        String?
   profile_id Int     @default(autoincrement()) @id
-  user_id    User
+  user_id    user
 }
-model User {
+model user {
   email    String    @default("") @unique
   name     String?
   role     String    @default("USER")
   user_id  Int       @default(autoincrement()) @id
-  posts    Post[]
-  profiles Profile[]
+  posts    post[]
+  profiles profile[]
 }
```

