CREATE table if not EXISTS artists (
    artist_id SERIAL PRIMARY KEY,
    artist_name VARCHAR(100) NOT NULL
);

-- Создание таблицы жанров
CREATE table if not EXISTS genres (
    genre_id SERIAL PRIMARY KEY,
    genre_name VARCHAR(50) NOT NULL
);

-- Создание таблицы для связи между исполнителями и жанрами
CREATE table if not EXISTS artist_genre (
    artist_id INT REFERENCES artists(artist_id),
    genre_id INT REFERENCES genres(genre_id),
    PRIMARY KEY (artist_id, genre_id)
);

-- Создание таблицы альбомов
create TABLE if  not exists albums (
	album_id SERIAL primary key,
	album_name VARCHAR(50) not null,
	album_date DATE not NULL
);

-- Создание таблицы для связи между исполнителями и альбомами
CREATE table if not EXISTS artist_album (
    artist_id INT REFERENCES artists(artist_id),
    album_id INT REFERENCES albums(album_id),
    PRIMARY KEY (artist_id, album_id)
);

--Создание таблицы сборников
create table if not exists compilations (
	compilation_id SERIAL primary key,
	compilation_name VARCHAR(50) not null,
	compilation_year DATE not null
);

--Создание таблицы сборников и артистов (многие ко многим)
CREATE table if not EXISTS compilation_artist (
    artist_id INT REFERENCES artists(artist_id),
    compilation_id INT REFERENCES compilations(compilation_id),
    PRIMARY KEY (artist_id, compilation_id)
);

-- Создание таблицы трэков "один ко многим" к альбомам
create table if not exists tracks(
	track_id SERIAL primary key,
	track_name VARCHAR(50) not null,
	track_len INT not null,
	album_id int references albums(album_id),
	artist_id INT REFERENCES artists(artist_id)
);

