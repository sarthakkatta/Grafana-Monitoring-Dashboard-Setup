# 🚀 Grafana Monitoring Dashboard Setup

Welcome to this **step-by-step beginner-friendly guide** on creating your **first Grafana Monitoring Dashboard**.

This guide uses **Prometheus + Grafana** to monitor your server's **health, CPU usage, memory usage, and disk usage**.

Perfect for **beginners in DevOps, Linux, and Cloud Monitoring**. 🌍

---

## 📌 Step 1: Open Query Editor

1. In your Grafana panel, you will see **Metric → Select metric** option.
2. Just above it, you will find the **Builder / Code toggle**.
3. Click on **Code** → A **textbox** will open where you can write queries.

---

## 📌 Step 2: First Panel — Instance Health

In the **Code box**, type:

```promql
up
```

* Go to **Legend** → set it as:

```text
{{instance}}
```

* For **Visualization** → Keep it as **Time series**.
* *(Optional: You can also select **Stat panel** for a simple view).*
* Click **Run queries → Apply** ✅

---

## 📌 Step 3: Second Panel — CPU Usage %

In **Code mode**, write this query:

```promql
100 - (avg by (instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
```

* Go to **Standard options** → **Unit** → Select:

```text
Percent (0–100%)
```

* Set **Legend** as:

```text
{{instance}}
```

* Run queries → Apply ✅

---

## 📌 Step 4: Third Panel — Memory Usage %

Add this query:

```promql
(1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) * 100
```

* Set **Unit** → **Percent**
* Set **Legend** as:

```text
{{instance}}
```

* Apply ✅

---

## 📌 Step 5: Fourth Panel — Disk Usage %

Use this query:

```promql
100 - ((node_filesystem_avail_bytes{fstype!~"tmpfs|squashfs"} / node_filesystem_size_bytes{fstype!~"tmpfs|squashfs"}) * 100)
```

* Set **Unit** → **Percent**
* Set **Legend** as:

```text
{{instance}} - {{mountpoint}}
```

* Apply ✅

---

## 📌 Step 6: Save Your Dashboard

1. On the top-right, click **Save Dashboard** (Blue Button).
2. Name it:

```text
My First Monitoring Dashboard
```

3. Save it ✅
4. Set **Time range** → Last 15 minutes.
5. Set **Auto-refresh** → 10s.

🎉 Congratulations! You have successfully created your **first Grafana Monitoring Dashboard**.
