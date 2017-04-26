# Rails API Relationships Diagnostic

Place your responses inside the fenced code-blocks where indivated by comments.

1.  Describe a reason why a join tables may be valuable.

  ```md
    To keep from duplicating data in your database.
  ```

1.  Provide a database table structure and explain the Entity Relationship that
  describes a many-to-many relationship for `Profiles`, `Movies` and `Favorites`
  (Think of Netflix). A `Profile` has a `given_name`, `surname` and `email` and a
  `Movies` have `title`, `release_date`, and `length` and `Favorites` would be the
  join table with references to `Movies` and `Profiles`.

  ```md
    The join table would be a many to many, where a profile can have many favorites
    and a movie can have many profiles through favorites
  ```

1.  For the above example, what needs to be added to the Model files?

  ```rb
  class Profile < ActiveRecord::Base
  has_many :movies, through :favorites
  end
  ```

  ```rb
  class Movie < ActiveRecord::Base
  has_many :profiles, through :favorites
  end
  ```

  ```rb
  class Favorite < ActiveRecord::Base
  belongs_to: movie
  belongs_to: profile
  end
  ```

1.  What is the purpose of a serializer? What would our `Profile` serializer look
like to show all movies favorited by a profile on
`http://localhost:3000/profiles/1`

  ```md
    The serializer iterates through objects based on a set of rules.
  ```

  ```rb
  class ProfileSerializer < ActiveModel::Serializer
  attributes :id, :given_name, :sur_name, :email
  end
  ```

1.  What would the command be to _scaffold_ out a **join table** for Favorites from
the above `Movies` and `Profiles`.

  ```sh
    bin/rails generate scaffold favorite references:movies references:profiles
  ```

1.  What is `Dependent: Destroy` and where/why would we use it?

  ```md
    Dependent destroy tells the system when records are related causing the
    deletion of a record to remove related records.
  ```

1.  Think of **ANY** example where you would have a one-to-many relationship as well
as a many-to-many relationship in an application. You only need to list the
description about the resources and how they relate to one another.

  ```md
    A band has many albums, but an album is only going to have one band (typically)
    The relationship could be modeled as a table for bands, and a table for albmums
    with a foriegn key on the album table holding the id of the band that made it.

    Using the example from above - movies and people. I person can have many
    favorite movies, and a movie can have many people that favorite it. This is
    best handled by a join table as described above. The join table belongs to
    both the movies and people. People have many movies through the favorites
    table and movies have many people through the favorites table. 
  ```
