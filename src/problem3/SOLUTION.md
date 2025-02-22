Provide your solution here:

## **6. Troubleshooting High Memory Usage in NGINX Load Balancer (Ubuntu 24.04)**

### **Step-by-Step Troubleshooting Guide**
1. **Check System Memory Usage:**
   ```bash
   free -m
   vmstat -s
   ```
   Identify if the high memory consumption is due to NGINX or another process.

2. **Analyze Running Processes:**
   ```bash
   ps aux --sort=-%mem | head -10
   ```
   Find out if NGINX is consuming the most memory.

3. **Check NGINX Worker Process Usage:**
   ```bash
   ps -eo pid,comm,%mem --sort=-%mem | grep nginx
   ```
   If a single worker process is using too much memory, it might indicate a configuration issue.

4. **Inspect NGINX Logs:**
   ```bash
   tail -f /var/log/nginx/access.log
   tail -f /var/log/nginx/error.log
   ```
   Look for excessive requests or errors that could be causing memory spikes.

5. **Check NGINX Configuration:**
   ```bash
   nginx -T | grep worker_processes
   ```
   - If `worker_processes` is too high, it may cause memory exhaustion.
   - Reduce it if necessary.

6. **Monitor Connections & Traffic:**
   ```bash
   netstat -an | grep :80 | wc -l
   ```
   If connections are too high, consider rate limiting or enabling caching.

7. **Restart NGINX to Free Up Memory:**
   ```bash
   systemctl restart nginx
   ```

### **Possible Causes & Fixes**
| **Cause** | **Impact** | **Fix** |
|-----------|-----------|---------|
| High number of requests | Exhausts memory, leads to failures | Enable caching, rate limit, or scale horizontally |
| Misconfigured NGINX worker processes | Excessive memory use | Optimize worker processes, adjust limits |
| Memory leak in a module | Gradual performance degradation | Identify faulty module, disable or update |
| Log file growth | Can consume disk space and memory | Rotate logs using logrotate |

---

This document ensures a robust trading system while providing a structured approach to troubleshooting high memory issues in NGINX on Ubuntu 24.04.

