# 分页查询

- SQL

    ```sql
    SELECT *
    FROM table_name
    LIMIT 10 OFFSET 0;
    ```

- RowBounds

    ```java
    RowBounds rowBounds = new RowBounds(0, 10); // (offset, limit)
    List<Book> books = sqlSession.selectList("book.queryAll", null, rowBounds);   
    ```

- MyBatis 实现

    1. Pagination
        
        ```java
        public class Pagination<T extends Serializable> implements Serializable {
            private List<T> list;
            private String statement;
            private int pageSize;
            private int totalRows;
            private int totalPages;
            private int currentPage;
    
            // constructors
            // setters & getters
        }
        ```
    2. `GenericDaoImpl`
        
        ```java
        /**
         * 分页查询
         *
         * @param statement   查询的 SQL 的 id
         * @param parameter   查询的参数
         * @param currentPage 当前的页码
         * @return Pagination 的实例
         */
        private Pagination<T> getPagination(String statement, Object parameter, int currentPage) {
            int totalRows = sqlSession.selectList(namespace.concat(".").concat(statement), parameter).size();
            int totalPages = (int) Math.ceil(totalRows / (double) Constant.PAGE_SIZE);
            RowBounds rowBounds = new RowBounds((currentPage - 1) * Constant.PAGE_SIZE, Constant.PAGE_SIZE);
            List<T> list = sqlSession.selectList(namespace.concat(".").concat(statement), parameter, rowBounds);
            return new Pagination<>(list, statement, Constant.PAGE_SIZE, totalRows, totalPages, currentPage);
        }
        ```