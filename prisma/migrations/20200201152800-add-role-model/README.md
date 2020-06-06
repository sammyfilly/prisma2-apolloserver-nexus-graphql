# Migration `20200201152800-add-role-model`

This migration has been generated by hatchli at 2/1/2020, 3:28:00 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
CREATE TABLE `prisma`.`posts` (
    `author_id` int NOT NULL ,
    `content` varchar(191)   ,
    `created_at` datetime(3)   ,
    `post_id` int NOT NULL  ,
    `title` varchar(191) NOT NULL DEFAULT '' ,
    PRIMARY KEY (`post_id`)
) 
DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `prisma`.`profiles` (
    `bio` varchar(191)   ,
    `profile_id` int NOT NULL  ,
    `user_id` int NOT NULL ,
    PRIMARY KEY (`profile_id`)
) 
DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE TABLE `prisma`.`users` (
    `email` varchar(191) NOT NULL DEFAULT '' ,
    `name` varchar(191)   ,
    `role` varchar(191) NOT NULL DEFAULT 'USER' ,
    `user_id` int NOT NULL  ,
    PRIMARY KEY (`user_id`)
) 
DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci

CREATE UNIQUE INDEX `users.email` ON `prisma`.`users`(`email`)

ALTER TABLE `prisma`.`posts` ADD FOREIGN KEY (`author_id`) REFERENCES `prisma`.`users`(`user_id`) ON DELETE RESTRICT

ALTER TABLE `prisma`.`profiles` ADD FOREIGN KEY (`user_id`) REFERENCES `prisma`.`users`(`user_id`) ON DELETE RESTRICT
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration ..20200201152800-add-role-model
--- datamodel.dml
+++ datamodel.dml
@@ -1,0 +1,36 @@
+generator client {
+  provider = "prisma-client-js"
+}
+
+datasource mysql {
+  provider = "mysql"
+  url      = "mysql://prisma:F1g+sparrow@prisma.clisj67py2b1.us-east-2.rds.amazonaws.com:3306/prisma"
+}
+
+model posts {
+  content    String?
+  created_at DateTime?
+  post_id    Int       @id
+  title      String
+  author_id  users
+}
+
+model profiles {
+  bio        String?
+  profile_id Int     @id
+  user_id    users
+}
+
+model users {
+  email      String     @unique
+  name       String?
+  user_id    Int        @id
+  postses    posts[]
+  profileses profiles[] 
+  role role @default(USER)
+}
+
+enum role {
+  USER
+  ADMIN
+}
```

