# Median

```sql
select * from db a, db b group by a.val having sum( sign( 1 - sign(b.val - a.val) ) ) = ( count(*) + 1 ) / 2;
```

