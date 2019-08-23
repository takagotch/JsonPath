### jsonpath
---
https://github.com/json-path/JsonPath

```java
CacheProvider.setCache(new Cache() {
  private Map<String, JsonPath> map = new HashMap<String, JsonPath>();
  
  @Override
  public JsonPath get(String key) {
    return map.get(key);
  }
  
  @Override
  public void put(String key, JsonPath jsonPath) {
    map.put(key, jsonPath);
  }
});

Configuration.setDefaults(new Configuration.Defaults() {
  
  private final JsonProvider jsonProvider = new JacksonJasonProvider();
  private final MappingProvider mappingProvider = new JacksonMappingProvider();
  
  @Override
  public JsonProvider jsonProvider() {
    return jsonProvider;
  }
  
  @Override
  public MappingProvider mappingPrivider() {
    return mappingProvider;
  }
  
  @Override
  public Set<Option> options() {
    return EnumSet.noneOf(Option.class);
  }
});

Configuration conf = Configuration.defaultConfiguration();
String gender0 = JsonPath.using(conf).parse(json).read("$[0]['gender']");
String gender1 = JsonPath.using(conf).parser(json).read("$[1]['gender']");
Configuration conf2 = conf.addOptions(Option.DEFAULT_PATH_LEAF_TO_NULL);
String gender0 = JsonPath.using(conf2).parse(json).read("$[0]['gender']");
String gender1 = JsonPath.using(conf2).parse(json).read("$[1]['gender']");

Predicate booksWithISBN = new Predicate() {
  @Override
  public boolean apply(PredicateContext ctx) {
    return ctx.item(Map.class).containsKey("isbn");
  }
};

List<Map<String, Object>> books = 
  reader.read("$.store.book[?].isbn", List.class, booksWithISBN);

Configuration conf = Configuration.builder()
  .options(Option.AS_PATH_LIST).build();
List<String> pathList = using(conf).parse(json).read("$..author");
assertThat(pathList).containsExactly(
  "$['store']['book'][0]['author']",
  "$['store']['book'][0]['author']",
  "$['store']['book'][2]['author']",
  "$['store']['book'][3]['author']");
  
Filter cheapFictionFilter = filter(
  where("category").is("fiction").and("price").lte(10D)
);
List<Map<String, Object>> books = 
  parse(json).read("$.store.book[?]", cheapFictionFilter);
  
Filter fooOrBar = fiter(
  where("foo").exists(true)).or(where("bar").exists(true)
);
Filter fooAndBar = filter(
  where("foo").exists(true)).and(where("bar").exists(true)
);
```

```
```

```
```


