# Kue Prom
Provides [promotheus](https://prometheus.io/) metrics for [Kue](https://github.com/Automattic/kue)

Metrics:
- inactive job (gauge)
- active job (gauge)
- complete job (gauge)
- failed job (gauge)
- delayed job (gauge)

## Usage
```typescript
import promClient from 'prom-client';
import * as kueProm from 'kue-prom';

const queue: kue.Queue = kue.createQueue(...);

const kueMetric = kueProm.init({
  jobName: 'pdf',
  queue,
  promClient, // optional, it will use internal prom client if it is not given
  interval: 1000, // optional, in ms, default to 60000
  prefixMetricName: 'my_app' // optional
});

kueMetric.run();

// Metrics result in Promotheus
// my_app_pdf_job_inactive
// my_app_pdf_job_active
// my_app_pdf_job_complete
// my_app_pdf_job_failed
// my_app_pdf_job_delayed
```

## API
### init(options)
Initialize

options:
- jobName (**required**): kue job name
- queue (**required**): kue queue
- promClient (*optional*): prom client instance
- interval (*optional*, default 60000): interval in ms to fetch the Kue statistic
- prefixMetricName (*optional*): prefix for metric name

### run()
Start running and fetching the data from Kue based on interval

### stop()
Stop running

## License
MIT © [Budi Irawan](https://github.com/deerawan)