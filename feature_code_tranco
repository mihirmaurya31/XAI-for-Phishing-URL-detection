using System;
using System.Collections.Concurrent;
using System.Collections.Generic;
using System.Diagnostics;
using System.Globalization;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Threading;
using System.Threading.Tasks;
using CsvHelper;
using CsvHelper.Configuration;

// Helper class to hold the results from the HEAD request.
public class HeadResult
{
    public int TimeResponse { get; set; } = -1;
    public int QtyRedirects { get; set; } = 0;
    public int HttpStatus { get; set; } = -1;
    public string ServerHeader { get; set; } = "";
    public int TlsSslCertificate { get; set; }
}

// Helper class to hold the results of a single-pass lexical scan on a string.
public class LexicalCounts
{
    public int QtyDot { get; set; }
    public int QtyHyphen { get; set; }
    public int QtyUnderline { get; set; }
    public int QtySlash { get; set; }
    public int QtyQuestionmark { get; set; }
    public int QtyEqual { get; set; }
    public int QtyAt { get; set; }
    public int QtyAnd { get; set; }
    public int QtyExclamation { get; set; }
    public int QtySpace { get; set; }
    public int QtyTilde { get; set; }
    public int QtyComma { get; set; }
    public int QtyPlus { get; set; }
    public int QtyAsterisk { get; set; }
    public int QtyHashtag { get; set; }
    public int QtyDollar { get; set; }
    public int QtyPercent { get; set; }
    public int Length { get; set; }
}

// The main data class, mapping directly to your desired CSV columns.
public class TrancoDataRow
{
    public string url { get; set; }
    public int Label { get; set; } = 0;
    public int qty_dot_url { get; set; }
    public int qty_hyphen_url { get; set; }
    public int qty_underline_url { get; set; }
    public int qty_slash_url { get; set; }
    public int qty_questionmark_url { get; set; }
    public int qty_equal_url { get; set; }
    public int qty_at_url { get; set; }
    public int qty_and_url { get; set; }
    public int qty_exclamation_url { get; set; }
    public int qty_space_url { get; set; }
    public int qty_tilde_url { get; set; }
    public int qty_comma_url { get; set; }
    public int qty_plus_url { get; set; }
    public int qty_asterisk_url { get; set; }
    public int qty_hashtag_url { get; set; }
    public int qty_dollar_url { get; set; }
    public int qty_percent_url { get; set; }
    public int length_url { get; set; }
    public int qty_dot_domain { get; set; }
    public int qty_hyphen_domain { get; set; }
    public int qty_underline_domain { get; set; }
    public int qty_slash_domain { get; set; }
    public int qty_questionmark_domain { get; set; }
    public int qty_equal_domain { get; set; }
    public int qty_at_domain { get; set; }
    public int qty_and_domain { get; set; }
    public int qty_exclamation_domain { get; set; }
    public int qty_space_domain { get; set; }
    public int qty_tilde_domain { get; set; }
    public int qty_comma_domain { get; set; }
    public int qty_plus_domain { get; set; }
    public int qty_asterisk_domain { get; set; }
    public int qty_hashtag_domain { get; set; }
    public int qty_dollar_domain { get; set; }
    public int qty_percent_domain { get; set; }
    public int domain_length { get; set; }
    public int qty_dot_directory { get; set; }
    public int qty_hyphen_directory { get; set; }
    public int qty_underline_directory { get; set; }
    public int qty_slash_directory { get; set; }
    public int qty_questionmark_directory { get; set; }
    public int qty_equal_directory { get; set; }
    public int qty_at_directory { get; set; }
    public int qty_and_directory { get; set; }
    public int qty_exclamation_directory { get; set; }
    public int qty_space_directory { get; set; }
    public int qty_tilde_directory { get; set; }
    public int qty_comma_directory { get; set; }
    public int qty_plus_directory { get; set; }
    public int qty_asterisk_directory { get; set; }
    public int qty_hashtag_directory { get; set; }
    public int qty_dollar_directory { get; set; }
    public int qty_percent_directory { get; set; }
    public int directory_length { get; set; }
    public int qty_dot_file { get; set; }
    public int qty_hyphen_file { get; set; }
    public int qty_underline_file { get; set; }
    public int qty_slash_file { get; set; }
    public int qty_questionmark_file { get; set; }
    public int qty_equal_file { get; set; }
    public int qty_at_file { get; set; }
    public int qty_and_file { get; set; }
    public int qty_exclamation_file { get; set; }
    public int qty_space_file { get; set; }
    public int qty_tilde_file { get; set; }
    public int qty_comma_file { get; set; }
    public int qty_plus_file { get; set; }
    public int qty_asterisk_file { get; set; }
    public int qty_hashtag_file { get; set; }
    public int qty_dollar_file { get; set; }
    public int qty_percent_file { get; set; }
    public int file_length { get; set; }
    public int qty_dot_params { get; set; }
    public int qty_hyphen_params { get; set; }
    public int qty_underline_params { get; set; }
    public int qty_slash_params { get; set; }
    public int qty_questionmark_params { get; set; }
    public int qty_equal_params { get; set; }
    public int qty_at_params { get; set; }
    public int qty_and_params { get; set; }
    public int qty_exclamation_params { get; set; }
    public int qty_space_params { get; set; }
    public int qty_tilde_params { get; set; }
    public int qty_comma_params { get; set; }
    public int qty_plus_params { get; set; }
    public int qty_asterisk_params { get; set; }
    public int qty_hashtag_params { get; set; }
    public int qty_dollar_params { get; set; }
    public int qty_percent_params { get; set; }
    public int params_length { get; set; }
    public int qty_dot_fragment { get; set; }
    public int qty_hyphen_fragment { get; set; }
    public int qty_underline_fragment { get; set; }
    public int qty_slash_fragment { get; set; }
    public int qty_questionmark_fragment { get; set; }
    public int qty_equal_fragment { get; set; }
    public int qty_at_fragment { get; set; }
    public int qty_and_fragment { get; set; }
    public int qty_exclamation_fragment { get; set; }
    public int qty_space_fragment { get; set; }
    public int qty_tilde_fragment { get; set; }
    public int qty_comma_fragment { get; set; }
    public int qty_plus_fragment { get; set; }
    public int qty_asterisk_fragment { get; set; }
    public int qty_hashtag_fragment { get; set; }
    public int qty_dollar_fragment { get; set; }
    public int qty_percent_fragment { get; set; }
    public int fragment_length { get; set; }
    public int time_response { get; set; }
    public int qty_redirects { get; set; }
    public int http_status { get; set; }
    public string server_header { get; set; }
    public int tls_ssl_certificate { get; set; }
}

public class Program
{
    // --- Configuration Constants ---
    private const string TRONCO_FILE = @"C:\Users\Mihir Maurya\Downloads\tranco_7NZNX.csv"; // Your input file
    private const string OUTPUT_FULL = @"C:\Users\Mihir Maurya\Downloads\tranco_dataset_full.csv"; // Your output file
    private const int HTTP_CONNECTIONS = 2000; // Concurrently processed URLs
    private static readonly TimeSpan HttpTimeout = TimeSpan.FromSeconds(4);

    // A single, reusable HttpClient instance is best practice for performance.
    private static readonly HttpClient client = new HttpClient(new HttpClientHandler { AllowAutoRedirect = false })
    {
        Timeout = HttpTimeout
    };

    /// <summary>
    /// HIGH-PERFORMANCE, SINGLE-PASS character counter. This is the core of the CPU-bound optimization.
    /// </summary>
    private static LexicalCounts CalculateLexicalFeatures(string text)
    {
        if (string.IsNullOrEmpty(text)) return new LexicalCounts();

        var counts = new LexicalCounts { Length = text.Length };
        foreach (char c in text)
        {
            switch (c)
            {
                case '.': counts.QtyDot++; break;
                case '-': counts.QtyHyphen++; break;
                case '_': counts.QtyUnderline++; break;
                case '/': counts.QtySlash++; break;
                case '?': counts.QtyQuestionmark++; break;
                case '=': counts.QtyEqual++; break;
                case '@': counts.QtyAt++; break;
                case '&': counts.QtyAnd++; break;
                case '!': counts.QtyExclamation++; break;
                case ' ': counts.QtySpace++; break;
                case '~': case '˜': counts.QtyTilde++; break;
                case ',': counts.QtyComma++; break;
                case '+': counts.QtyPlus++; break;
                case '*': counts.QtyAsterisk++; break;
                case '#': counts.QtyHashtag++; break;
                case '$': counts.QtyDollar++; break;
                case '%': counts.QtyPercent++; break;
            }
        }
        return counts;
    }

    /// <summary>
    /// Performs an asynchronous HTTP HEAD request for a single URL.
    /// </summary>
    private static async Task<HeadResult> HeadWorkerAsync(string url)
    {
        var normalizedUrl = url.StartsWith("http") ? url : $"http://{url}";
        var result = new HeadResult
        {
            TlsSslCertificate = normalizedUrl.StartsWith("https://", StringComparison.OrdinalIgnoreCase) ? 1 : 0
        };

        try
        {
            var stopwatch = Stopwatch.StartNew();
            using (var request = new HttpRequestMessage(HttpMethod.Head, normalizedUrl))
            using (var response = await client.SendAsync(request, HttpCompletionOption.ResponseHeadersRead))
            {
                stopwatch.Stop();
                result.TimeResponse = (int)stopwatch.ElapsedMilliseconds;
                result.HttpStatus = (int)response.StatusCode;
                result.QtyRedirects = response.Headers.Location != null ? 1 : 0;
                result.ServerHeader = response.Headers.Server?.ToString() ?? "";
            }
        }
        catch (Exception) { /* Default values will be used on failure */ }
        return result;
    }

    /// <summary>
    /// Fetches URL metadata in parallel with real-time progress reporting.
    /// </summary>
    private static async Task<List<HeadResult>> FetchHeadFeaturesParallel(IReadOnlyList<string> urls, int maxWorkers)
    {
        var results = new ConcurrentDictionary<int, HeadResult>();
        long processedCount = 0;
        int totalUrls = urls.Count;

        using (var semaphore = new SemaphoreSlim(maxWorkers, maxWorkers))
        {
            var tasks = new List<Task>(urls.Count);
            for (int i = 0; i < urls.Count; i++)
            {
                await semaphore.WaitAsync();
                int index = i;
                tasks.Add(Task.Run(async () =>
                {
                    try
                    {
                        results[index] = await HeadWorkerAsync(urls[index]);
                    }
                    finally
                    {
                        semaphore.Release();
                        // --- PROGRESS REPORTING (THREAD-SAFE) ---
                        long currentCount = Interlocked.Increment(ref processedCount);
                        double percentage = (double)currentCount / totalUrls * 100;
                        // Use carriage return '\r' to overwrite the line
                        Console.Write($"\rFetching HEAD features: {percentage:F2}% complete ({currentCount}/{totalUrls})   ");
                    }
                }));
            }
            await Task.WhenAll(tasks);
        }

        // Move to the next line after the progress bar is finished.
        Console.WriteLine();
        return Enumerable.Range(0, totalUrls).Select(i => results.TryGetValue(i, out var res) ? res : new HeadResult()).ToList();
    }

    public static async Task Main(string[] args)
    {
        Console.WriteLine($"Process started at {DateTime.Now:F}");
        var stopwatch = Stopwatch.StartNew();

        // Reading the file can be parallelized for a small boost on very large files
        var urls = File.ReadLines(TRONCO_FILE)
                       .AsParallel()
                       .Select(line => $"http://{line.Split(',')[1]}")
                       .ToList();
        Console.WriteLine($"Read {urls.Count} URLs from '{TRONCO_FILE}'.");

        // --- Stage 1: Network I/O with progress ---
        var headFeatures = await FetchHeadFeaturesParallel(urls, HTTP_CONNECTIONS);
        Console.WriteLine("Finished fetching HEAD features.");

        // --- Stage 2: CPU Processing with progress ---
        Console.WriteLine($"Building all lexical features in parallel on {Environment.ProcessorCount} CPU cores...");
        var dataToProcess = urls.Zip(headFeatures, (url, head) => new { Url = url, Head = head });
        long processedLexicalCount = 0;
        int totalUrlCount = urls.Count;

        var finalRows = dataToProcess
            .AsParallel()
            .WithDegreeOfParallelism(Environment.ProcessorCount)
            .Select(item =>
            {
                var row = new TrancoDataRow { url = item.Url };

                #region Deconstruct URL and Calculate All Lexical Features
                string domain = "", directory = "", file = "", query = "", fragment = "";
                try
                {
                    var uri = new Uri(item.Url);
                    domain = uri.Host;
                    directory = uri.AbsolutePath;
                    file = Path.GetFileName(directory); // Can be empty if no file part
                    query = uri.Query;
                    fragment = uri.Fragment;
                }
                catch (UriFormatException) { /* Leave parts empty for malformed URLs */ }

                var urlCounts = CalculateLexicalFeatures(item.Url);
                var domainCounts = CalculateLexicalFeatures(domain);
                var dirCounts = CalculateLexicalFeatures(directory);
                var fileCounts = CalculateLexicalFeatures(file);
                var paramsCounts = CalculateLexicalFeatures(query);
                var fragmentCounts = CalculateLexicalFeatures(fragment);

                // --- Map URL features ---
                row.length_url = urlCounts.Length; row.qty_dot_url = urlCounts.QtyDot; row.qty_hyphen_url = urlCounts.QtyHyphen; row.qty_underline_url = urlCounts.QtyUnderline; row.qty_slash_url = urlCounts.QtySlash; row.qty_questionmark_url = urlCounts.QtyQuestionmark; row.qty_equal_url = urlCounts.QtyEqual; row.qty_at_url = urlCounts.QtyAt; row.qty_and_url = urlCounts.QtyAnd; row.qty_exclamation_url = urlCounts.QtyExclamation; row.qty_space_url = urlCounts.QtySpace; row.qty_tilde_url = urlCounts.QtyTilde; row.qty_comma_url = urlCounts.QtyComma; row.qty_plus_url = urlCounts.QtyPlus; row.qty_asterisk_url = urlCounts.QtyAsterisk; row.qty_hashtag_url = urlCounts.QtyHashtag; row.qty_dollar_url = urlCounts.QtyDollar; row.qty_percent_url = urlCounts.QtyPercent;

                // --- Map Domain features ---
                row.domain_length = domainCounts.Length; row.qty_dot_domain = domainCounts.QtyDot; row.qty_hyphen_domain = domainCounts.QtyHyphen; row.qty_underline_domain = domainCounts.QtyUnderline; row.qty_slash_domain = domainCounts.QtySlash; row.qty_questionmark_domain = domainCounts.QtyQuestionmark; row.qty_equal_domain = domainCounts.QtyEqual; row.qty_at_domain = domainCounts.QtyAt; row.qty_and_domain = domainCounts.QtyAnd; row.qty_exclamation_domain = domainCounts.QtyExclamation; row.qty_space_domain = domainCounts.QtySpace; row.qty_tilde_domain = domainCounts.QtyTilde; row.qty_comma_domain = domainCounts.QtyComma; row.qty_plus_domain = domainCounts.QtyPlus; row.qty_asterisk_domain = domainCounts.QtyAsterisk; row.qty_hashtag_domain = domainCounts.QtyHashtag; row.qty_dollar_domain = domainCounts.QtyDollar; row.qty_percent_domain = domainCounts.QtyPercent;

                // --- Map Directory features ---
                row.directory_length = dirCounts.Length; row.qty_dot_directory = dirCounts.QtyDot; row.qty_hyphen_directory = dirCounts.QtyHyphen; row.qty_underline_directory = dirCounts.QtyUnderline; row.qty_slash_directory = dirCounts.QtySlash; row.qty_questionmark_directory = dirCounts.QtyQuestionmark; row.qty_equal_directory = dirCounts.QtyEqual; row.qty_at_directory = dirCounts.QtyAt; row.qty_and_directory = dirCounts.QtyAnd; row.qty_exclamation_directory = dirCounts.QtyExclamation; row.qty_space_directory = dirCounts.QtySpace; row.qty_tilde_directory = dirCounts.QtyTilde; row.qty_comma_directory = dirCounts.QtyComma; row.qty_plus_directory = dirCounts.QtyPlus; row.qty_asterisk_directory = dirCounts.QtyAsterisk; row.qty_hashtag_directory = dirCounts.QtyHashtag; row.qty_dollar_directory = dirCounts.QtyDollar; row.qty_percent_directory = dirCounts.QtyPercent;

                // --- Map File features ---
                row.file_length = fileCounts.Length; row.qty_dot_file = fileCounts.QtyDot; row.qty_hyphen_file = fileCounts.QtyHyphen; row.qty_underline_file = fileCounts.QtyUnderline; row.qty_slash_file = fileCounts.QtySlash; row.qty_questionmark_file = fileCounts.QtyQuestionmark; row.qty_equal_file = fileCounts.QtyEqual; row.qty_at_file = fileCounts.QtyAt; row.qty_and_file = fileCounts.QtyAnd; row.qty_exclamation_file = fileCounts.QtyExclamation; row.qty_space_file = fileCounts.QtySpace; row.qty_tilde_file = fileCounts.QtyTilde; row.qty_comma_file = fileCounts.QtyComma; row.qty_plus_file = fileCounts.QtyPlus; row.qty_asterisk_file = fileCounts.QtyAsterisk; row.qty_hashtag_file = fileCounts.QtyHashtag; row.qty_dollar_file = fileCounts.QtyDollar; row.qty_percent_file = fileCounts.QtyPercent;

                // --- Map Params features ---
                row.params_length = paramsCounts.Length; row.qty_dot_params = paramsCounts.QtyDot; row.qty_hyphen_params = paramsCounts.QtyHyphen; row.qty_underline_params = paramsCounts.QtyUnderline; row.qty_slash_params = paramsCounts.QtySlash; row.qty_questionmark_params = paramsCounts.QtyQuestionmark; row.qty_equal_params = paramsCounts.QtyEqual; row.qty_at_params = paramsCounts.QtyAt; row.qty_and_params = paramsCounts.QtyAnd; row.qty_exclamation_params = paramsCounts.QtyExclamation; row.qty_space_params = paramsCounts.QtySpace; row.qty_tilde_params = paramsCounts.QtyTilde; row.qty_comma_params = paramsCounts.QtyComma; row.qty_plus_params = paramsCounts.QtyPlus; row.qty_asterisk_params = paramsCounts.QtyAsterisk; row.qty_hashtag_params = paramsCounts.QtyHashtag; row.qty_dollar_params = paramsCounts.QtyDollar; row.qty_percent_params = paramsCounts.QtyPercent;

                // --- Map Fragment features ---
                row.fragment_length = fragmentCounts.Length; row.qty_dot_fragment = fragmentCounts.QtyDot; row.qty_hyphen_fragment = fragmentCounts.QtyHyphen; row.qty_underline_fragment = fragmentCounts.QtyUnderline; row.qty_slash_fragment = fragmentCounts.QtySlash; row.qty_questionmark_fragment = fragmentCounts.QtyQuestionmark; row.qty_equal_fragment = fragmentCounts.QtyEqual; row.qty_at_fragment = fragmentCounts.QtyAt; row.qty_and_fragment = fragmentCounts.QtyAnd; row.qty_exclamation_fragment = fragmentCounts.QtyExclamation; row.qty_space_fragment = fragmentCounts.QtySpace; row.qty_tilde_fragment = fragmentCounts.QtyTilde; row.qty_comma_fragment = fragmentCounts.QtyComma; row.qty_plus_fragment = fragmentCounts.QtyPlus; row.qty_asterisk_fragment = fragmentCounts.QtyAsterisk; row.qty_hashtag_fragment = fragmentCounts.QtyHashtag; row.qty_dollar_fragment = fragmentCounts.QtyDollar; row.qty_percent_fragment = fragmentCounts.QtyPercent;
                #endregion

                // --- Map HTTP features ---
                row.http_status = item.Head.HttpStatus;
                row.time_response = item.Head.TimeResponse;
                row.qty_redirects = item.Head.QtyRedirects;
                row.server_header = item.Head.ServerHeader;
                row.tls_ssl_certificate = item.Head.TlsSslCertificate;

                // --- PROGRESS REPORTING (THREAD-SAFE) ---
                long currentCount = Interlocked.Increment(ref processedLexicalCount);
                // Update the console periodically to avoid performance overhead from too many writes.
                if (currentCount % 1000 == 0 || currentCount == totalUrlCount)
                {
                    double percentage = (double)currentCount / totalUrlCount * 100;
                    Console.Write($"\rBuilding lexical features: {percentage:F2}% complete ({currentCount}/{totalUrlCount})   ");
                }

                return row;
            })
            .ToList();

        // Move to the next line after the progress bar is finished.
        Console.WriteLine();
        Console.WriteLine("Finished building all features.");

        // Writing to CSV is fast and done sequentially at the end.
        using (var writer = new StreamWriter(OUTPUT_FULL))
        using (var csv = new CsvWriter(writer, CultureInfo.InvariantCulture))
        {
            csv.WriteRecords(finalRows);
        }

        stopwatch.Stop();
        Console.WriteLine($"\n✅ Done! Wrote {finalRows.Count} rows to '{OUTPUT_FULL}' in {stopwatch.Elapsed.TotalSeconds:F2} seconds.");
    }
