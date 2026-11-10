# Google Patents and BigQuery

This workshop introduces Google Patents and the Google Patents Public Datasets in BigQuery as tools for searching and analyzing patent information.

We will begin with the Google Patents web interface to search for patents and explore the information available in individual patent records. We will then use Google BigQuery to access patent data with SQL.

Participants are encouraged to modify the example searches and queries to investigate technologies, inventors, organizations, or research areas that interest them.

## Google Patents

[Google Patents](https://patents.google.com/)

We will begin by using the Google Patents interface to search for patents and examine individual records.

Some useful information to look for includes:

- Patent and publication numbers
- Application numbers
- Inventors
- Assignees
- Filing and publication dates
- Patent classifications
- Citations
- Related patent applications and patent families
- Patent documents and drawings

Try searching for a technology or research area that interests you. You can also search for inventors, organizations, and known patent identifiers.

After exploring patent records through the web interface, we will look at how patent information is represented in BigQuery.

## BigQuery

Google makes large patent datasets available through Google BigQuery. BigQuery allows us to query these datasets using SQL rather than retrieving individual records through an API.

The examples below use the following table:

```text
patents-public-data.patents.publications
```

The goal is not to learn SQL from the beginning. Instead, we will use familiar SQL operations to explore patent information.

### Using the BigQuery Sandbox

The BigQuery Sandbox provides access to BigQuery without requiring a paid Google Cloud account.

The BigQuery Explorer can also be used to examine the tables and fields available in the patent datasets.

### Available Fields in the Patents Publications Table

Before working with a dataset, it can be useful to see what fields are available.

The following query lists the fields in the `patents.publications` table.

```sql
SELECT 
  column_name, 
  data_type, 
  is_nullable
FROM 
  `patents-public-data.patents.INFORMATION_SCHEMA.COLUMNS`
WHERE 
  table_name = 'publications';
```

You can also explore the table schema directly through the BigQuery Explorer.

### Search for an Inventor

The following example searches for recent U.S. patent records containing an inventor named Boushey.

```sql
SELECT 
  publication_number,
  filing_date,
  ARRAY_TO_STRING(inventor, ', ') AS inventors
FROM 
  `patents-public-data.patents.publications`
WHERE 
  country_code = 'US'
  AND filing_date >= 20200101
  AND EXISTS (
    SELECT 1 
    FROM UNNEST(inventor) AS inv_name 
    WHERE LOWER(inv_name) LIKE '%boushey%'
  )
LIMIT 10;
```

Try replacing `boushey` with another inventor name.

The `inventor` field can contain multiple values. BigQuery's `UNNEST()` function allows us to work with values contained inside repeated fields.

### Retrieve a Known Patent

We can also retrieve a patent when we already know its identifier.

The following example retrieves an older U.S. patent with the publication number `US-208521-A`.

```sql
SELECT 
  publication_number,
  filing_date,
  publication_date,
  ARRAY_TO_STRING(inventor, ', ') AS inventors,
  title_localized
FROM 
  `patents-public-data.patents.publications`
WHERE 
  publication_number LIKE 'US-208521%';
```

This patent provides an interesting example of differences between search systems. The patent is available in Google Patents, but searches for the inventor name do not reliably retrieve it through the Google Patents search interface.

Once we know the publication identifier, however, we can retrieve the record directly:

[US208521A in Google Patents](https://patents.google.com/patent/US208521A/en)

This is a useful reminder that a search interface does not necessarily expose every record that exists in the underlying collection. Search results can depend on database coverage, metadata, indexing, search fields, and the search strategy being used.

BigQuery provides another way to investigate the underlying patent data.

### Create a Google Patents Link From BigQuery

Notice that BigQuery represents the publication number as `US-208521-A`, while Google Patents uses `US208521A` in its URL.

We can remove the hyphens and construct a Google Patents link directly from the BigQuery record.

```sql
SELECT 
  publication_number,
  CONCAT(
    'https://patents.google.com/patent/',
    REPLACE(publication_number, '-', ''),
    '/en'
  ) AS google_patents_url
FROM 
  `patents-public-data.patents.publications`
WHERE 
  publication_number = 'US-208521-A';
```

This provides one way to move from records discovered or analyzed in BigQuery back to individual patents in Google Patents.

### Search a Technology Area

We can also use BigQuery to search patent titles for a technology or research area.

The following example searches U.S. patent titles for `supply chain`.

```sql
SELECT
  publication_number,
  filing_date,
  publication_date,
  ARRAY_TO_STRING(inventor, ', ') AS inventors,
  title_localized
FROM
  `patents-public-data.patents.publications`
WHERE
  country_code = 'US'
  AND EXISTS (
    SELECT 1
    FROM UNNEST(title_localized) AS title
    WHERE LOWER(title.text) LIKE '%supply chain%'
  )
LIMIT 50;
```

Try replacing `supply chain` with a technology or research area that interests you.

Consider whether the returned patents appear relevant to the topic you intended to search.

### Explore Patent Classifications

Patent records can contain Cooperative Patent Classification (CPC) codes describing their technological subject matter.

The following example counts frequently occurring CPC codes among recent U.S. patent records.

```sql
SELECT
  cpc.code AS cpc_code,
  COUNT(*) AS patent_count
FROM
  `patents-public-data.patents.publications`,
  UNNEST(cpc) AS cpc
WHERE
  country_code = 'US'
  AND filing_date >= 20200101
GROUP BY
  cpc_code
ORDER BY
  patent_count DESC
LIMIT 20;
```

Some questions to consider:

- What do the most common CPC codes represent?
- At what level of the CPC hierarchy are we looking?
- How might CPC classifications help define a technology area?
- How could we combine keyword searching with patent classifications?

## Try Your Own Investigation

Modify the example queries to investigate something related to your own research, work, or interests.

You might begin with:

- A technology
- An inventor
- An organization
- A patent number
- A CPC classification
- A research area

You can also move back and forth between Google Patents and BigQuery.

For example:

1. Search for a technology in Google Patents.
2. Examine several relevant patents.
3. Notice the terminology and CPC classifications used in those patents.
4. Use those terms or classifications in BigQuery.
5. Examine patterns across a larger collection of records.
6. Return to Google Patents to investigate interesting individual patents.

The results from one information system can help guide searches and analysis in another.

## What We Did

In this workshop, we used Google Patents to search for and examine individual patent records and BigQuery to work with patent information using SQL.

The examples included:

- Exploring the structure of the patent dataset
- Searching for an inventor
- Retrieving a known patent
- Connecting BigQuery records to Google Patents
- Searching patents by technology
- Exploring CPC classifications

These examples are starting points rather than complete patent landscape analyses. They can be modified and extended to investigate research and technology areas of interest.
