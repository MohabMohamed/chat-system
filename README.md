# Chat System

## Getting Started

To get you a copy of the production version of the project up and running on your local machine
download the submodules and setup the production.env files as in the [contribution guide](./CONTRIBUTION.md) then run:

```shell script
docker-compose up -d --force-recreate
```

## Contribution

check [contribution guide](./CONTRIBUTION.md)

## Apis

check [api guide](./API.md)

## Challenging parts

### chats_count and messages_count in DB

Solve it by using cronjobs as I defined a rake task and setup it as a cronjob by running [whenever gem](https://github.com/javan/whenever) in docker-entrypoint.sh as the last step for running the container.

### Make the chats and messages writes on mysql as little as possible

For this problem I decided to use bulk insert to make the writes as little as possible. But faced another problem is to maintain `per_app_id` and `per_chat_id` and the first naive solution to come to my head is to maintain it at the application level and locking the queue that's responsible for storing the data until it's written but this solution would be bad if we ran more than one instance of our service.

The second solution to come into me is using `MyISAM` engine for `chats` and `messages` tables as it enables me to specify AUTO_INCREMENT on a secondary column in a multiple-column index. As stated in is documentation :

`For MyISAM tables, you can specify AUTO_INCREMENT on a secondary column in a multiple-column index. In this case, the generated value for the AUTO_INCREMENT column is calculated as MAX(auto_increment_column) + 1 WHERE prefix=given-prefix. This is useful when you want to put data into ordered groups.`

That solution would be performant but at some downsides like `MyISAM` don't support foreign keys, relationship constraints and transactions.

The third solution was to define triggers for inserting new chat or new message that handle that columns and in `InnoDB`
if the trigger performs a write it locks the table implicitly for `WRITE` , that's right this solution will be a little slower than the second but won't have any other downside.

## Leftout work

Adding swagger documentation (open-api) and specs for remaining endpoints (did it for application endpoints only). And caching some endpoints results using redis .
