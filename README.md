# SphinxTuner

SphinxTuner is a performance analysis tool for [SphinxSearch](https://sphinxsearch.com/), designed to help you optimize your Sphinx configuration and improve search performance. Inspired by tools like `mysqltuner`, this utility analyzes key metrics, checks configuration parameters, and provides actionable recommendations to enhance the efficiency of your Sphinx setup.

---

## Features

- **Comprehensive Analysis**: Evaluates critical performance metrics such as query execution time, memory usage, and index size.
- **Configuration Validation**: Checks and validates important Sphinx configuration parameters (`mem_limit`, `workers`, `net_workers`, `max_matches`, etc.) based on [Sphinx 3.x documentation](https://sphinxsearch.com/docs/sphinx3.html).
- **Performance Recommendations**: Provides detailed suggestions to optimize Sphinx performance, including memory allocation, thread settings, and I/O performance tuning.
- **Multi-threading Support**: Analyzes `workers` and `net_workers` settings to ensure optimal utilization of multi-core CPUs and network handling.
- **Query Optimization**: Highlights slow queries and suggests enabling query caching or external caching (e.g., Redis, Memcached).
- **System Resource Monitoring**: Tracks RAM and disk usage to prevent overloading your server.

- ---

## Installation

1. **Prerequisites**:
   - Ensure SphinxSearch is installed and running on your system.
   - Install the MySQL client (`mysql`) to connect to SphinxQL via port `9306`.

   ```bash
   sudo apt update
   sudo apt install mysql-client
   ```
2. **Download SphinxTuner**:
   ```bash
   wget https://raw.githubusercontent.com/asfed/sphinxtuner/main/sphinxtuner
   chmod +x sphinxtuner
   ```
3. **Run the Script**:
  ```bash
  ./sphinxtuner
  ```

---

## Usage

### Example Output

```plaintext
SphinxTuner v1.0
-------------------------
System Information:
Total RAM: 16384 MB
Sphinx Uptime: 12 hours 34 minutes
Connections: 10111
Queries Executed: 129116
Average Query Time: 0.001 seconds
RAM Used by Sphinx: 43.5 MB
Index Size on Disk: 127.4 MB

Configuration Details:
mem_limit: 4G
indexer threads: 8
workers: Not set
net_workers: Not set
max_matches: 1000
read_timeout: 5.000
write_timeout: 5.000
max_iops: 40
max_iosize: 1M
query_log_format: sphinxql
query_cache_size: Not set

Performance Analysis:
Warning: workers parameter is not set. Consider setting it to 'threads' for better performance with multiple cores.
Warning: net_workers parameter is not set. Consider setting it to a value greater than 0 for improved network handling.
Warning: query_cache_size is not set. Consider enabling query caching for frequently executed queries.

Optimization Recommendations:
- Increase mem_limit to a value greater than the disk index size (127.4 MB).
- Use RT indexes for fast data updates if possible.
- Enable external caching with Redis or Memcached for frequently executed queries.
- Review and optimize your queries by analyzing the query logs (query.log).
- Adjust max_iops and max_iosize settings in sphinx.conf for better I/O performance.
- Set workers to 'threads' for better utilization of multi-core CPUs.
- Set net_workers to a value greater than 0 for improved network handling.
- Increase max_matches to at least 1000 for large datasets.
- Set read_timeout and write_timeout to at least 5 seconds for stability.
- Enable query_cache_size for caching frequently executed queries.

Analysis completed. Use the recommendations above to improve Sphinx performance.
```

---

## Key Parameters Analyzed

The following Sphinx configuration parameters are analyzed and optimized:

| Parameter         | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| `mem_limit`       | Memory limit for indexing and searching. Should exceed the index size.     |
| `workers`         | Multi-threading mode (`threads` recommended for modern systems).            |
| `net_workers`     | Number of threads for network handling.                                    |
| `max_matches`     | Maximum number of matches returned per query.                              |
| `read_timeout`    | Timeout for read operations.                                               |
| `write_timeout`   | Timeout for write operations.                                              |
| `max_iops`        | Maximum I/O operations per second.                                         |
| `max_iosize`      | Maximum size of I/O operations.                                            |
| `query_cache_size`| Enables query caching for frequently executed queries.                     |

For more details, refer to the [Sphinx 3.x Documentation](https://sphinxsearch.com/docs/sphinx3.html).

---

## Recommendations

- **Increase `mem_limit`**: Ensure it exceeds the size of your disk indexes.
- **Enable Query Caching**: Use `query_cache_size` or external caching (Redis/Memcached) for frequently executed queries.
- **Optimize Threads**: Set `workers` to `threads` and configure `net_workers` for better performance.
- **Monitor Logs**: Regularly review `query.log` for slow queries and optimize them.


---

## Contributing

Contributions are welcome! If you have ideas for improvements or bug fixes, feel free to open an issue or submit a pull request.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Links

- [SphinxSearch Official Website](https://sphinxsearch.com/)
- [Sphinx 3.x Documentation](https://sphinxsearch.com/docs/sphinx3.html)

   
