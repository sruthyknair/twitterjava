# twitterjava


public void run()
{
    List<StreamListener> listners= new ArrayList<>();
    listeners.add(this)
    twitter.streamingOperations().sample(listners);
    
}
@postConstruct
public void afterPropertiesSet() throws Exception{
    if(processingEnabled)
    {
        for(int i=0;i<taskExecutor.getMaxpoolsize();i++)
        {
            taskExecutor.execute(new TweetProcessor(graphService,queue));
        }
        run();
    }
}
@override
public void onTweet(Tweet tweet)
{
    queue.offer(tweet);
}


@override
public void run()
{
    while(true)
    {
        try
        {
            Tweet tweet=queue.take();
            processTweet(tweet);
        }
        catch(InterruptedException e)
        {
            e.printStackTrace();
        }
    }
}
