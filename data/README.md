## Instructions to read in the data by API

I used API method to obtain my datasets from CDC. 

First, you have to create an account with password. 

Then, you have to apply for a free app token. 

Last, copy your API Endpoint.

Here are my datasets links:

`https://chronicdata.cdc.gov/500-Cities-Places/500-Cities-Obesity-among-adults-aged-18-years/bjvu-3y7d`

`https://chronicdata.cdc.gov/500-Cities-Places/500-Cities-Diagnosed-diabetes-among-adults-aged-18/cn78-b9bj`

```{r}
dia <- read.socrata(
  "https://chronicdata.cdc.gov/resource/cn78-b9bj.json?year=2017",
  app_token = "bEkVW73ASzmTkZ9riAtf2YS5c",
  email     = "clu74108@usc.edu",
  password  = "your_password"
)
dia <- as.data.table(dia)
write.csv(dia,"./data/dia.csv", row.names = F)
```

```{r}
obe <- read.socrata(
  "https://chronicdata.cdc.gov/resource/bjvu-3y7d.json?year=2017",
  app_token = "bEkVW73ASzmTkZ9riAtf2YS5c",
  email     = "clu74108@usc.edu",
  password  = "your_password"
)
obe <- as.data.table(obe)
write.csv(obe,"./data/obe.csv", row.names = F)
```

<br>

This is the URL to download the Physical Inactivity dataset:

`https://www.cdc.gov/physicalactivity/data/inactivity-prevalence-maps/tables/2020/1-self-reported.csv`

```{r message=FALSE, echo=FALSE, warning=FALSE}
if (!file.exists("1-self-reported.csv"))
  download.file(
    url = "https://www.cdc.gov/physicalactivity/data/inactivity-prevalence-maps/tables/2020/1-self-reported.csv",
    destfile = "1-self-reported.csv",
    method   = "libcurl",
    timeout  = 60
  )
physical_inactivity <- fread("1-self-reported.csv")
write.csv(physical_inactivity,"./data/1-self-reported.csv", row.names = F)
```

<br>


