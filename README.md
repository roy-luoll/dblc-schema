# dblc-schema
database schema definition language

This language is designed to define database layer schema in text, thus can be bound with domain class, offering convenience of version management, including tracking, comaparing and validating of a specified version of database.

The language is simple enough and provide mapping to popular database management systems.

sample snippet is as follows:

database db_connection {
  fieldtype {  // here define dbms-specific mapping
    boolean  "number(1)";
    int16    "number(4)";
    int32    "number(8)";
    int64    "number(15)";
    double   "number(19.6)";
    float    "number(12.5)";
    string   "varchar2";
    date     "date";
    time     "time";
    datetime "timestamp";
  };

  table employee (physical 'zg.employee') // define table
  {
    value_bool   boolean;
    vaue_i16     int16 nullable;
    vaue_i32     int32;
    vaue_i64     int64;
    vaue_float   float;
    value_double double;
    value_string varchar(255);
    birthday     date;
    meeting_time time;
    event_timestamp datetime;

    [partition(vaue_i16)];  // define partition, that is very important for huge-number records table
    [primary key(vaue_i32)]; // primary and indices.
    [index idxByTime(event_timestamp)];
    [index cidxXXX(vaue_i16,value_string)];
  };
}
