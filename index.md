---
layout: post
---

<html lang="en">
	<head>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<meta http-equiv="x-ua-compatible" content="ie=edge">
		<meta name="description" content="Entity Framework Plus | BulkSaveChanges | Bulk Insert, Update, Delete and Merge | Query Cache | Query Filter | Query Include | Query Future | Query IncludeFilter | Audit">
		<meta name="keywords" content="BulkSaveChanges | Bulk Insert, Update, Delete and Merge | Query Cache | Query Filter | Query Future | Query IncludeFilter | Audit">
		<meta name="msvalidate.01" content="89359D9C492A475C0061398008D105FB" />
		<title>Entity Framework Plus | Bulk Operations & Utilities</title>
		<link rel="icon" type="image/png" href="http://entityframework-plus.net/images/logo.png">
		<link rel="stylesheet" type="text/css" href="https://cdn.rawgit.com/twbs/bootstrap/v4-dev/dist/css/bootstrap.min.css">
		<link rel="stylesheet" type="text/css" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css">
		<!-- todo: change me !-->
		<link rel="stylesheet" type="text/css" href="http://entityframework-plus.net/css/github.css">
	</head>
	
	<body>
  
		<!-- anchor !-->
		<a id="download" href="#"></a>
		<a id="github" href="#"></a>
		
		<!-- top-header !-->
		<div id="top-header">
			<div class="container">
				<div class="text-right">
					<a href="mailto:info@zzzprojects.com"><i class="fa fa-envelope"></i>&nbsp;&nbsp;info@zzzprojects.com</a>
					<a href="https://www.facebook.com/zzzprojects" target="_blank"><i class="fa fa-facebook"></i></a>
					<a href="https://twitter.com/zzzprojects" target="_blank"><i class="fa fa-twitter"></i></a>
					<a href="https://plus.google.com/+Zzzprojects_NetSQL/posts" target="_blank"><i class="fa fa-google-plus"></i></a>
					<a href="http://zzzprojects.us9.list-manage.com/subscribe?u=cecbc4775cf67bf1ff82018af&id=4765ffa5f8" target="_blank" class="hidden-sm-down"><i class="fa fa-newspaper-o"></i></a>
				</div>
			</div>
		</div>
		
		<!-- header !-->
		<header>
			<div class="container">
				<div class="row">
					<div class="col-lg-6">
						<div class="card">
							<div class="card-block">
								<h1 class="card-title">EntityFramework Plus (EF+)</h1>
								<h3>Entity Framework Bulk Operations & Utilities</h3>
								<hr class="m-y-md" />
								<div class="lead">
									<a href="https://github.com/zzzprojects/EntityFramework-Plus/wiki/Downloads" target="_blank" class="btn btn-success btn-lg btn-left" role="button"><span><i class="fa fa-cloud-download fa-2x"></i>&nbsp;<span>Download</span></span></a>
									<a href="https://github.com/zzzprojects/EntityFramework-Plus" target="_blank" class="btn btn-primary btn-lg btn-right" role="button"><span><i class="fa fa-github fa-2x"></i>&nbsp;<span>GitHub</span></span></a>
									<p class="text-muted">* FREE Version limited to 50 characters</p>						
								</div>
							</div>
						</div>
					</div>
					<div class="col-lg-6">
						<div class="card">
							<div class="card-block card-contents">
								<ul>
									<li>Bulk Operations</li>
										<ul>
											<li><a href="#ef-bulk-operations">Bulk SaveChanges</a>/li>
											<li><a href="#ef-bulk-operations">Bulk Insert</a></li>
											<li><a href="#ef-bulk-operations">Bulk Update</a>/li>
											<li><a href="#ef-bulk-operations">Bulk Delete</a>/li>
											<li><a href="#ef-bulk-operations">Bulk Merge</a>/li>
										</ul>
									<li>Batch Operations</li>
										<ul>
											<li><a href="#ef-batch-delete">Batch Delete</a>/li>
											<li><a href="#ef-batch-update">Batch Update</a></li>
										</ul>
									</li>
									<li>Query
										<ul>
											<li><a href="#ef-query-cache">Query Cache</a></li>
											<li><a href="#ef-query-deferred">Query Deferred</a></li>
											<li><a href="#ef-query-filter">Query Filter</a></li>
											<li><a href="#ef-query-future">Query Future</a></li>
											<li><a href="#ef-query-includefilter">Query IncludeFilter</a></li>
											<li><a href="#ef-query-includeoptimized">Query IncludeOptimized</a></li>
										</ul>
									</li>
									<li>Audit</li>
								</ul>
							</div>
						</div>
					</div>
				</div>
			</div>
		</header>
		
		<!-- anchor !-->
		<a id="features" href="#"></a>
		
		<!-- features !-->
		<div id="feature">
		
			<!-- feature EF+ Query Cache !-->
			<a id="ef-query-cache" href="#"></a>
			<div class="container">
				<h3>Query Cache</h3>
				<p class="font-weight-bold">Query cache is the second level cache for Entity Framework.</p>
				<p>The result of the query is returned from the cache. If the query is not cached yet, the query is materialized and cached before being returned.</p>
				<p>You can specify cache policy and cache tag to control CacheItem expiration.</p>
				<p>Supports:</p>
				<p class="font-italic">Cache Policy</p>
{% highlight csharp %}
// The query is cached using default QueryCacheManager options
var countries = ctx.Countries.Where(x => x.IsActive).FromCache();

// (EF5 | EF6) The query is cached for 2 hours
var states = ctx.States.Where(x => x.IsActive).FromCache(DateTime.Now.AddHours(2));

// (EF7) The query is cached for 2 hours without any activity
var options = new MemoryCacheEntryOptions() { SlidingExpiration = TimeSpan.FromHours(2)};
var states = ctx.States.Where(x => x.IsActive).FromCache(options);
{% endhighlight %}
				<p class="font-italic">Cache Tags</p>
{% highlight csharp %}
var states = db.States.Where(x => x.IsActive).FromCache("countries", "states");
var stateCount = db.States.Where(x => x.IsActive).DeferredCount().FromCache("countries", "states");

// Expire all cache entry using the "countries" tag
QueryCacheManager.ExpireTag("countries");
{% endhighlight %}
				<a class="btn btn-primary btn-lg" href="https://github.com/zzzprojects/EntityFramework-Plus/wiki/EF-Query-Cache-%7C-Entity-Framework-Second-Level-Caching" role="button" target="_blank">Learn More&nbsp;<i class="fa fa-hand-o-right"></i></a>
			</div>
		
			<!-- feature EF+ Query Deferred !-->
			<a id="ef-query-deferred" href="#"></a>
			<div class="container">
				<h3>Query Deferred</h3>
				<p class="font-weight-bold">Defer the execution of a query which is normally executed to allow some features like Query Cache and Query Future.</p>
{% highlight csharp %}
// Oops! The query is already executed, we cannot use Query Cache or Query Future features
var count = ctx.Customers.Count();

// Query Cache
ctx.Customers.DeferredCount().FromCache();

// Query Future
ctx.Customers.DeferredCount().FutureValue();
{% endhighlight %}
				<a class="btn btn-primary btn-lg" href="https://github.com/zzzprojects/EntityFramework-Plus/wiki/EF-Query-Deferred-%7C-Entity-Framework-deferring-immediate-LINQ-query-execution" role="button" target="_blank">Learn More&nbsp;<i class="fa fa-hand-o-right"></i></a>
			</div>
			
			<!-- feature EF+ Query Filter !-->
			<a id="ef-query-filter" href="#"></a>
			<div class="container">
				<h3>Query Filter</h3>
				<p class="font-weight-bold">Filter query with predicate at global, instance or query level.</p>
				<p>Supports:</p>
				<p class="font-italic">Global Filter</p>
{% highlight csharp %}
// CREATE global filter
QueryFilterManager.Filter<Customer>(x => x.Where(c => c.IsActive));

var ctx = new EntityContext();

// TIP: Add this line in EntitiesContext constructor instead
QueryFilterManager.InitilizeGlobalFilter(ctx);

// SELECT * FROM Customer WHERE IsActive = true
var customer = ctx.Customers.ToList();
{% endhighlight %}
				<p class="font-italic">Instance Filter</p>
{% highlight csharp %}
var ctx = new EntityContext();

// CREATE filter
ctx.Filter<Customer>(x => x.Where(c => c.IsActive));

// SELECT * FROM Customer WHERE IsActive = true
var customer = ctx.Customers.ToList();
{% endhighlight %}
				<p class="font-italic">Query Filter</p>
{% highlight csharp %}
var ctx = new EntityContext();

// CREATE filter disabled
ctx.Filter<Customer>(CustomEnum.EnumValue, x => x.Where(c => c.IsActive), false);

// SELECT * FROM Customer WHERE IsActive = true
var customer = ctx.Customers.Filter(CustomEnum.EnumValue).ToList();
{% endhighlight %}
				<a class="btn btn-primary btn-lg" href="https://github.com/zzzprojects/EntityFramework-Plus/wiki/EF-Query-Filter-%7C-Entity-Framework-Dynamic-Instance-and-Global-Filters" role="button" target="_blank">Learn More&nbsp;<i class="fa fa-hand-o-right"></i></a>
			</div>
			
			<!-- feature EF+ Query Future !-->
			<a id="ef-query-future" href="#"></a>
			<div class="container">
				<h3>Query Future</h3>
				<p class="font-weight-bold">Query Future allow to reduce database roundtrip by batching multiple queries in the same sql command.</p>
				<p>All future query are stored in a pending list. When the first future query require a database roundtrip, all query are resolved in the same sql command instead of making a database roundtrip for every sql command.</p>
				<p>Supports:</p>
				<p class="font-italic">Future</p>
{% highlight csharp %}
// GET the states & countries list
var futureCountries = db.Countries.Where(x => x.IsActive).Future();
var futureStates = db.States.Where(x => x.IsActive).Future();

// TRIGGER all pending queries (futureCountries & futureStates)
var countries = futureCountries.ToList();
{% endhighlight %}
				<p class="font-italic">FutureValue</p>
{% highlight csharp %}
// GET the first active customer and the number of avtive customers
var futureFirstCustomer = db.Customers.Where(x => x.IsActive).DeferredFirstOrDefault().FutureValue();
var futureCustomerCount = db.Customers.Where(x => x.IsActive).DeferredCount().FutureValue();

// TRIGGER all pending queries (futureFirstCustomer & futureCustomerCount)
Customer firstCustomer = futureFirstCustomer.Value;
{% endhighlight %}
				<a class="btn btn-primary btn-lg" href="https://github.com/zzzprojects/EntityFramework-Plus/wiki/EF-Query-Future-%7C-Entity-Framework-Combine-and-Execute-Multiple-SQL-Command" role="button" target="_blank">Learn More&nbsp;<i class="fa fa-hand-o-right"></i></a>
			</div>
		</div>
		
		<!-- anchor !-->
		<a id="pro" href="#"></a>
		
		<!-- pricing !-->
		<div id="pricing">
			<div class="container">
				<div class="row">
					<div class="col-lg-6">
						<h2>Pricing</h2>
						<hr class="m-y-md" />
						<p>Become a <span class="text-bold text-green">PRO</span> now and start saving time and money!</p>
						<p>Thousands of <span class="text-bold">development hours</span> and thousands of <span class="text-bold">unit tests</span> to make EF+ the best and most robust third party library for Entity Framework.</p>
						<p>Compatible with license: <a href="http://www.zzzprojects.com/products/dotnet-development/entity-framework-extensions/" target="_blank">.NET Entity Framework Extensions</a></p>
						<hr class="m-y-md" />
						<p>Every month, a new monthly trial of the PRO Version is available to let you evaluate all its features without limitations.</p>					
					</div>
					<div class="col-lg-6">
						<table class="table table-hover table-bordered">
							<thead class="thead-inverse">
								<tr>
									<th></th>
									<th>FREE</th>
									<th>PRO</th>
								</tr>
							</thead>
							<tbody>
								<tr>
									<th>Bulk SaveChanges</th>
									<td><i class="fa fa-times fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Bulk Insert</th>
									<td><i class="fa fa-times fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Bulk Update</th>
									<td><i class="fa fa-times fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Bulk Delete</th>
									<td><i class="fa fa-times fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Bulk Merge</th>
									<td><i class="fa fa-times fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Audit</th>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Batch Delete</th>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Batch Update</th>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Query Cache</th>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
							    <tr>
									<th>Query Deferred</th>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Query Filter</th>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Query Future</th>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Query IncludeFilter</th>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Query IncludeOptimized</th>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Commercial License</th>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Royalty-Free</th>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
								<tr>
									<th>Support & Upgrades (1 year)</th>
									<td><i class="fa fa-times fa-2x"></i></td>
									<td><i class="fa fa-check-square-o fa-2x"></i></td>
								</tr>
							</tbody>
						</table>
						
						<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top" onsubmit="return purchase_validate()">
							<input type="hidden" name="cmd" value="_s-xclick">
							<input type="hidden" name="hosted_button_id" value="GY8E58XJPDGLW">
							<input type="hidden" name="currency_code" value="USD">
							<fieldset class="form-group">
								<input type="hidden" name="on0" value="Seats">
								<select name="os0" class="form-control">
									<option value="1 seat">EntityFramework Plus $599 (1 seat)</option>
									<option value="2-4 seats" selected>EntityFramework Plus $799 (2-4 seats)</option>
									<option value="5-9 seats">EntityFramework Plus $999 (5-9 seats)</option>
									<option value="10-14 seats">EntityFramework Plus $1199 (10-14 seats)</option>
									<option value="15-19 seats">EntityFramework Plus $1399 (15-19 seats)</option>
								</select> 
							</fieldset>
							<div class="checkbox">
								<label>
									<input id="agree_agreement" type="checkbox">I have read and agree to the <a href="http://www.zzzprojects.com/license-agreement/" target="_blank">License Agreement</a>.
								</label>
							</div>
							<button type="submit" class="btn btn-success btn-lg"><span><i class="fa fa-shopping-cart"></i>&nbsp;<span>BUY NOW</span></span></button>
							<div><br />* Contact us for invoice or payment method alternative.</div>
						</form>					
					</div>
				</div>
			</div>
			
			<!-- validation !-->
			<div id="error_validation" class="modal fade" tabindex="-1" role="dialog" aria-labelledby="modal_agreement" aria-hidden="true">
				<div class="modal-dialog" role="document">
					<div class="modal-content">
						<div class="modal-header">
							<h4 class="modal-title" id="modal_agreement">License Agreement</h4>
						</div>
						<div class="modal-body bg-danger">
							You must read and agree to the License Agreement.
						</div>
						<div class="modal-footer">
							<button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
						</div>
					</div>
				</div>
			</div>
		</div>
		
		<!-- support !-->
		<div id="support">
			<div class="container">
				<h2>Test our Outstanding Support</h2>
				<h3>We usually answer within the next business day, hour, or minutes!</h3>
				<div class="row">
					<hr class="hidden-sm-up" />
					<div class="col-sm-6 col-lg-3">
						<div class="card">
							<div class="card-block">
								<h4 class="card-title">Documentation</h4>
							</div>
							<a href="https://github.com/zzzprojects/EntityFramework-Plus/wiki" target="_blank"><i class="fa fa-folder-open fa-5x"></i></a>
							<div class="card-block">
								<p class="card-text">Consult our complete documentation to help you getting started.</p>
								<a href="https://github.com/zzzprojects/EntityFramework-Plus/wiki" target="_blank">Documentation</a>
							</div>
						</div>
					</div>
					<hr class="hidden-sm-up" />
					<div class="col-sm-6 col-lg-3">
						<div class="card">
							<div class="card-block">
								<h4 class="card-title">Contact Us</h4>
							</div>
							<a href="mailto:info@zzzprojects.com"><i class="fa fa-users fa-5x"></i></a>
							<div class="card-block">
								<p class="card-text">Email our team for any type of questions. We love to hear from you!</p>
								<a href="mailto:info@zzzprojects.com">info@zzzprojects.com</a>
							</div>
						</div>
					</div>
					<hr class="hidden-sm-up" />
					<div class="col-sm-6 col-lg-3">
						<div class="card">
							<div class="card-block">
								<h4 class="card-title">Forum</h4>
							</div>
							<a href="https://github.com/zzzprojects/EntityFramework-Plus/issues" target="_blank"><i class="fa fa-weixin fa-5x"></i></a>
							<div class="card-block">
								<p class="card-text">Visit the forum to propose new features or to discuss about the library.</p>
								<a href="https://github.com/zzzprojects/EntityFramework-Plus/issues" target="_blank">Forum</a>
							</div>
						</div>
					</div>
					<hr class="hidden-sm-up" />
					<div class="col-sm-6 col-lg-3">
						<div class="card">
							<div class="card-block">
								<h4 class="card-title">Open Source</h4>
							</div>
							<a href="https://github.com/zzzprojects/EntityFramework-Plus" target="_blank"><i class="fa fa-github fa-5x"></i></a>
							<div class="card-block">
								<p class="card-text">Access the source of the library you're using to understand better its logic.</p>
								<a href="https://github.com/zzzprojects/EntityFramework-Plus" target="_blank">GitHub</a>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>

		<!-- other product !-->
		<div id="product">
			<div class="container">
				<div class="row">
					<div class="col-lg-3">
						<h3>Entity Framework</h3>
						<ul>
							<li><a href="http://www.zzzprojects.com/products/dotnet-development/entity-framework-extensions/" target="_blank">Entity Framework Extensions</a></li>
							<li><a href="https://github.com/zzzprojects/EntityFramework-Plus" target="_blank">Entity Framework Plus (EF+)</a></li>
						</ul>
					</div>
					<div class="col-lg-3">
						<h3>Bulk Operations</h3>
						<ul>
							<li><a href="http://www.zzzprojects.com/products/dotnet-development/entity-framework-extensions/" target="_blank">.NET Entity Framework Extensions</a></li>
							<li><a href="http://www.zzzprojects.com/products/dotnet-development/bulk-operations/" target="_blank">.NET Bulk Operations</a></li>
						</ul>
					</div>
					<div class="col-lg-3">
						<h3>Expression Evaluator</h3>
						<ul>
							<li><a href="http://eval-sql.net/" target="_blank">Eval SQL.NET</a></li>
							<li><a href="http://eval-expression.net/" target="_blank">Eval Expression.NET</a></li>
						</ul>
					</div>
					<div class="col-lg-3">
						<h3>Others</h3>
						<ul>
							<li><a href="http://www.zzzprojects.com/products/dotnet-development/extension-methods/" target="_blank">Extension Methods</a></li>
							<li><a href="https://github.com/zzzprojects/LINQ-Async" target="_blank">LINQ Async</a></li>
						</ul>
					</div>
				</div>
			</div>		
		</div>
		
		<!-- footer !-->
		<footer>
			<div class="container text-center-md-down">
				<div class="row">
					<div class="col-lg-6">
						Copyright © <a href="http://www.zzzprojects.com/" target="_blank" class="text-bold">ZZZ Projects Inc.</a> 2014 - 2016
						<div class="hidden-lg-up"></div>
						All rights reserved
					</div>
					<hr class="hidden-lg-up" />
					<div class="col-lg-6 text-right-lg-up social">
						<a href="https://www.facebook.com/zzzprojects" target="_blank"><i class="fa fa-facebook"></i></a>
						<a href="https://twitter.com/zzzprojects" target="_blank"><i class="fa fa-twitter"></i></a>
						<a href="https://plus.google.com/+Zzzprojects_NetSQL/posts" target="_blank"><i class="fa fa-google-plus"></i></a>
						<a href="http://zzzprojects.us9.list-manage.com/subscribe?u=cecbc4775cf67bf1ff82018af&id=4765ffa5f8" target="_blank"><i class="fa fa-newspaper-o"></i></a>
					</div>
				</div>
			</div>
		</footer>

	<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
	<script type="text/javascript" src="https://cdn.rawgit.com/twbs/bootstrap/v4-dev/dist/js/bootstrap.min.js"></script>
	<script type="text/javascript">
	  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
	  (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
	  m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
	  })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

	  ga('create', 'UA-55584370-6', 'auto');
	  ga('send', 'pageview');
	  
	  function purchase_validate() {
		if($("#agree_agreement").prop('checked')) {
			return true;
		}
		
		$("#error_validation").modal('show')
		return false;
	  }
	</script>
	</body>
</html>

<style>
/* general */
* {
	 font-family: "Bitter",Georgia,"Times New Roman",serif;
}
.highlight * {
	font-family: Consolas, "Liberation Mono", Menlo, Courier, monospace;
}
.text-bold {
	font-weight: 700;
}
.text-green {
	color: rgb(68, 157, 68);
}
@media (max-width: 61em) {
	.text-center-md-down {
		text-align: center;
	}
}
@media (max-width: 33em) {
	.text-center-xs-down {
		text-align: center;
	}
}
@media (min-width: 62em) {
	.text-right-lg-up {
		text-align: right;
	}
}

/* section general */
#top-header {
	background-color: #111;
	border-bottom: 1px solid #000;
	font-size: 14px;
	padding: 5px 0px;
}
header {
	background: -moz-linear-gradient(top, #222, #333);
    background: -webkit-linear-gradient(top, #222, #333);
    background: -ms-linear-gradient(top, #222, #333);
    background: -o-linear-gradient(top, #222, #333);
    background: linear-gradient(top, #222, #333);
	border-bottom: 1px solid #111;
	border-top: 1px solid #333;
	padding: 40px 0px;
}
#announcement {
	background-color: #c00;
	color: #f1f1f1;
	font-weight: 700;
	font-style: italic;
	padding: 5px; 0px;
}
#feature {
    background: -moz-linear-gradient(top, #ddd, #f2f2f2);
    background: -webkit-linear-gradient(top, #ddd, #f2f2f2);
    background: -ms-linear-gradient(top, #ddd, #f2f2f2);
    background: -o-linear-gradient(top, #ddd, #f2f2f2);
    background: linear-gradient(top, #ddd, #f2f2f2);
	border-bottom: 1px solid #ddd;
    border-top: 1px solid #eee;
	padding-bottom: 60px;
}
#pricing {
	background-color: #fefefe;
	padding-top: 60px;
	padding-bottom: 60px;
}
#support {
	background: -moz-linear-gradient(top, #eee, #bbb);
    background: -webkit-linear-gradient(top, #eee, #bbb);
    background: -ms-linear-gradient(top, #eee, #bbb);
    background: -o-linear-gradient(top, #eee, #bbb);
    background: linear-gradient(top, #eee, #bbb);
	padding-top: 60px;
	padding-bottom: 60px;
	border-bottom: 1px solid #aaa;
	border-top: 1px solid #ccc;
}
#product {
    background: -moz-linear-gradient(top, #111, #222);
    background: -webkit-linear-gradient(top, #111, #222);
    background: -ms-linear-gradient(top, #111, #222);
    background: -o-linear-gradient(top, #111, #222);
    background: linear-gradient(top, #111, #222);
	border-bottom: 1px solid #111;
	border-top: 1px solid #333;
	color: #fefefe;
	padding: 20px 0px;
}
footer {
	background: -moz-linear-gradient(top, #333, #222);
    background: -webkit-linear-gradient(top, #333, #222);
    background: -ms-linear-gradient(top, #333, #222);
    background: -o-linear-gradient(top, #333, #222);
    background: linear-gradient(top, #333, #222);
	border-top: 1px solid #444;
	color: #666;
	padding-top: 5px;
	padding-bottom: 5px;
}

/* top-header */
#top-header a {
	color: #fefefe;
	padding-left: 10px;
	padding-right: 10px;
	text-decoration: none;
} 
#top-header a:hover {
	opacity: 0.7;
    transition: all 0.4s ease-in-out 0s;
}

/* header */
header .card {
	background-color: transparent;
	border: none;
	color: #f1f1f1;
}
header .card h1 {
	font-size: 3.0rem;
}
header .card h3 {
	font-size: 1.3rem;
}
header .card hr {
	border-color: initial;
}
header .card .lead .btn {
	width: 175px;
}
header .card .lead .btn-left {
	margin-right: 20px;
}
header .card .lead .btn span {
	display: inline-block;
	height: 40px;
}
header .card .lead .btn span span {
	vertical-align : middle;
}
header .card .lead .text-muted {
	font-size: 14px;
	padding-top: 10px;
}
header .card .card-code {
	background-color: #f1f1f1;
	border: 2px solid #444;
	color: #000;
	min-height: 350px;
}
header .card .card-code {
	padding: 0px;
}
header .card .card-code .highlight,
header .card .card-code .highlight pre {
	background-color: transparent;
	border: none;
}
header .card .card-contents {
	font-size: 18px;
}

header .card .card-contents a {
	color: #f1f1f1;
}

header .card .card-contents a:hover {
	opacity: 0.7;
	text-decoration: none;
    transition: all 0.4s ease-in-out 0s;
}

@media (max-width: 33em) {
	header .card h1 {
		font-size: 2.5rem;
	}
	header .card .lead .btn {
		margin-bottom: 20px;
	}
}

/* feature */
#feature h2 {
	font-size: 42px;
	letter-spacing: 4px;
	padding-top: 60px;
}
#feature h3 {
	border-bottom: 2px solid #000;
	letter-spacing: 3px;
	font-size: 36px;
	margin-bottom: 20px;
	padding-top: 60px;
	padding-bottom: 10px;
}
#feature .btn {
	margin-top: 40px;
}
@media (min-width: 62em) {
	#feature .row .col-lg-6:first-child {
		padding-right: 45px;
	}
	#feature .row .col-lg-6:last-child {
		padding-left: 45px;
	}
}

/* pricing */
#pricing h2 {
	margin-bottom: -10px;
}
#pricing .table thead th {
	text-align: center;
}
#pricing .table td {
	text-align: center;
}
#pricing .fa-times {
	color: #c9302c;
}
#pricing .fa-check-square-o {
	color: #449D44;
}

/* support */
#support {
	text-align: center;
}
#support h2 {
	padding-bottom: 20px;
}
#support h3 {
	font-size: 20px;
	padding-bottom: 40px;
}
#support .card {
	border: 0.0625rem solid #ccc;
}
#support .card-text {
	min-height: 75px;
}
#support i {
	color: #0275d8;
}

/* product */
#product h3 {
	letter-spacing: 1px;
	font-size: 18px;
	font-weight: 700;
}
#product ul {
	list-style: none;
	padding-left: 0px;
}
#product ul li {
	padding-top: 5px;
}
#product a {
	color: #999;
	font-size: 14px;
	letter-spacing: 0.5px;
}
#product a:hover {
	color: #fefefe;
	opacity: 0.9;
	text-decoration: none;
    transition: all 0.4s ease-in-out 0s;
}

/* footer */
@media (max-width: 61em) {
  footer {
	padding: 20px 0;
  }
}
footer hr {
	border-color: #666;
	margin: 20px;
}
footer a {
	color: #666;
}
footer a:hover {
	color: #666;
	opacity: 0.7;
	text-decoration: none;
    transition: all 0.4s ease-in-out 0s;
}
footer .social a {
	font-size: 24px;
	padding: 0px 10px;
}
</style>
