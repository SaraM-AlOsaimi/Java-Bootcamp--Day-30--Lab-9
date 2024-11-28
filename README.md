create database twitter;

create table users(
    user_id int primary key ,
    username varchar(15) not null unique ,
    email varchar(20) not null unique ,
    password varchar(8) not null unique ,
    created_at datetime default current_timestamp,
    bio varchar(100)
);

create table tweets(
    tweet_id int primary key ,
    user_id int,
    content varchar(200),
    created_at datetime ,
    updated_at datetime,
    foreign key (user_id) references  users (user_id)
);

create table likes(
    like_id int primary key ,
    user_id int,
    tweet_id int,
    created_at datetime,
    foreign key (user_id) references  users (user_id),
    foreign key (tweet_id) references  tweets (tweet_id)
);

create table comments(
    comment_id int primary key ,
    user_id int,
    tweet_id int,
    content varchar(150),
    created_at datetime,
    foreign key (user_id) references  users (user_id),
    foreign key (tweet_id) references  tweets (tweet_id)
);

create table retweets(
    retweet_id int primary key ,
    user_id int,
    tweet_id int,
    created_at datetime,
    foreign key (user_id) references  users (user_id),
    foreign key (tweet_id) references  tweets (tweet_id)
);

insert into users values(1,'sara123','sara123@gmail.com','sara@123',current_timestamp,'');
insert into users values(2,'mohammed098','mohammed@gmail.com','mohamd98',current_timestamp,'hi');
insert into users values(3,'fahad211','fahad@gmail.com','fa123123','2018-10-10T18:30:00','hello this fahed an d i user twitter');
insert into users values(4,'alaa123','alaa@gmail.com','alaa123','2019-09-15T09:50:00','');

select * from users;

insert into tweets (tweet_id, user_id, content, created_at, updated_at) values (1,1,'Just finished an amazing book! Can''t wait to dive into the next one.',current_timestamp,current_timestamp);
insert into tweets (tweet_id, user_id, content, created_at, updated_at) values (2,2,'Excited about the weekend! Time to relax and recharge.',current_timestamp,current_timestamp);
insert into tweets (tweet_id, user_id, content, created_at, updated_at) values (3,3,'Feeling grateful for the small things in life.','2019-10-10T18:30:00',current_timestamp);
insert into tweets (tweet_id, user_id, content, created_at, updated_at) values (4,4,'Learning something new every day. Today’s lesson: patience.','2020-11-12T12:00:00',current_timestamp);
insert into tweets (tweet_id, user_id, content, created_at, updated_at) values (5,1,'Had the best coffee this morning. Why does coffee always taste better when it’s shared?',current_timestamp,current_timestamp);

select * from tweets;

insert into retweets (retweet_id, user_id, tweet_id, created_at) values
(1, 1, 2, current_timestamp),
(2, 4, 5, current_timestamp),
(3, 2, 3, current_timestamp);

select * from retweets;

insert into likes (like_id, user_id, tweet_id, created_at) values
(1, 1, 2, current_timestamp),
(2, 2, 3, current_timestamp),
(3, 3, 5, current_timestamp),
(4, 4, 1, current_timestamp);

select * from likes;

insert into comments (comment_id, user_id, tweet_id, content, created_at) values
(1, 1, 2, 'I totally agree! Weekend vibes are the best.', current_timestamp),
(2, 3, 1, 'That book sounds interesting! What was it about?', current_timestamp),
(3, 2, 3, 'Gratitude is everything. We should all be thankful for the little things.', current_timestamp),
(4, 4, 1, 'I love coffee too! It does taste better with company.', current_timestamp);

select * from comments;

update users set username='fahd77' where  user_id=3;
update users set bio='Explorer of new ideas,and always up for an adventure.' where user_id=1;
update users set bio='Tech enthusiast, coffee lover, and always seeking new adventures. Let''s explore the world!' where user_id=4;

select * from users;

delete from comments where comment_id=3;
delete from comments where comment_id=1;

delete from likes where like_id=2;
delete from likes where like_id=1;

delete from retweets where retweet_id=1;
delete from retweets where retweet_id=3;

delete from tweets where tweet_id=2;

delete from users where user_id=2;

select * from users;
