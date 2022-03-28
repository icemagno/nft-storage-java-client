# nft-storage-java-client
A Java client for nft.storage API
```
  private void init(){
	    ApiClient defaultClient = Configuration.getDefaultApiClient();
	    defaultClient.setBasePath("https://api.nft.storage");
	    HttpBearerAuth bearerAuth = (HttpBearerAuth) defaultClient.getAuthentication("bearerAuth");
	    bearerAuth.setBearerToken( key );
	    this.api = new NftStorageApi(defaultClient);
  }
      
	private void store( String fileNamePath ) throws Exception {
	    String result = api.store( new File( fileNamePath ) );
	}
	

	private void storeSynch( String fileNamePath) throws Exception {
	    api.storeAsync( new File( fileNamePath ), new ApiCallback<String>() {
			@Override
			public void onUploadProgress(long bytesWritten, long contentLength, boolean done) {
				//
			}
			@Override
			public void onSuccess(String result, int statusCode, Map<String, List<String>> responseHeaders) {
				System.out.println( new JSONObject(result).toString(5) );
			}
			@Override
			public void onFailure(ApiException e, int statusCode, Map<String, List<String>> responseHeaders) {
				e.printStackTrace();
			}
			@Override
			public void onDownloadProgress(long bytesRead, long contentLength, boolean done) {
				//
			}
		});
	}
	
	private void status( String cid ) throws Exception {
	    String result = api.status( cid );
	    System.out.println( new JSONObject(result).toString(5) );	    
	}
	
	private void list() throws Exception {
		OffsetDateTime before = OffsetDateTime.now(); // OffsetDateTime | Return results created before provided timestamp
		Integer limit = 10; // Integer | Max records to return
		String result = api.list(before, limit);
		System.out.println( new JSONObject(result).toString(5) );		
	}	
```      
