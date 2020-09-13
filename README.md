# Github repos sort by stars

### Where I get these data?

Use below query on Google public github archive dataset:

```sql
SELECT repo.name
  , MAX(CAST(JSON_EXTRACT_SCALAR(payload, '$.pull_request.base.repo.stargazers_count')AS INT64)) stars
FROM `githubarchive.month.201912`  
WHERE JSON_EXTRACT_SCALAR(payload, '$.pull_request.base.repo.language') = 'Ruby'
AND type='PullRequestEvent'
GROUP by repo.name
ORDER BY stars DESC
```

##### References

* [BigQuery for GitHub : How to get most starred repo with a specific language](https://stackoverflow.com/questions/59887185/bigquery-for-github-how-to-get-most-starred-repo-with-a-specific-language)
* [madnight/githut](https://github.com/madnight/githut)
* [igrigorik/gharchive.org](https://github.com/igrigorik/gharchive.org)
* [GH Archive](http://www.gharchive.org/)