============
Introduction
============

Developing an Android app includes a number of repetitive tasks.
Like SQLite interactions or Model <=> JSON conversions or
``findViewsById()`` and then casting.

Eventually I ended up with a number of helper classes that were
copied from project to project. That's how DroidParts started.

The vision for DroidParts is a minimalistic framework
with clean API that eliminates the most common boilerplate code.

Some Code
=========

The code below:

#. Displays a list of Postings from ``EntityCursorAdapter`` which is backed by ORM.
#. Injects a ``Button`` and sets ``OnClickListener``.
#. Fetches, caches & attaches pics in a single line of code.
#. Serializes Postings to JSON & http POSTs the resulting ``JSONArray``.

.. code-block:: java

   public class PostingListFragment extends ListFragment implements
         View.OnClickListener, AlterableContent<Select<Posting>>,
         AsyncTaskResultListener<HTTPResponse> {
   
      private EntityCursorAdapter<Posting> adapter;
   
      @InjectDependency
      private DialogFactory dialogFactory;
   
      @InjectView(id = R.id.btn_submit, click = true)
      private Button submitBtn;
   
      private Select<Posting> select;
   
      @Override
      public void onActivityCreated(Bundle savedInstanceState) {
         super.onActivityCreated(savedInstanceState);
         adapter = new PostingCursorAdapter(getActivity());
         setListAdapter(adapter);
      }
   
      @Override
      public void onClick(View v) {
         if (v == submitBtn) {
            submitPostings();
         }
      }
   
      @Override
      public void setContent(Select<Posting> select) {
         this.select = select;
         adapter.changeData(select);
      }
   
      private void submitPostings() {
         new SubmitPostingsTask(getActivity(), this, select).execute();
      }
   
      @Override
      public void onAsyncTaskSuccess(HTTPResponse resp) {
         dialogFactory.showToast("Response: " + resp.body);
      }
   
      @Override
      public void onAsyncTaskFailure(Exception e) {
         L.w(e);
         dialogFactory.showErrorToast();
      }
   
   }
   
   public class PostingCursorAdapter extends EntityCursorAdapter<Posting> {
   
      public PostingCursorAdapter(Context ctx) {
         super(Posting.class, ctx);
      }
   
      @InjectDependency
      private ImageFetcher imageFetcher;
   
      @Override
      public void bindView(Context context, View view, Posting item) {
         PostingViewHolder holder = (PostingViewHolder) view.getTag();
         holder.titleView.setText(item.title);
         imageFetcher.attachImage(holder.iconView, item.iconUrl);
      }
   
      // ...
   }
   
   public class SubmitPostingsTask extends SimpleAsyncTask<HTTPResponse> {
   
      private final Select<Posting> select;
   
      private final EntityManager<Posting> entityManager;
      private final JSONSerializer<Posting> jsonSerializer;
   
      @InjectDependency
      private RESTClient2 restClient;
   
      public SubmitPostingsTask(Context ctx,
            AsyncTaskResultListener<HTTPResponse> resultListener,
            Select<Posting> select) {
         super(ctx, resultListener);
         this.select = select;
         entityManager = new EntityManager<Posting>(Posting.class, ctx);
         jsonSerializer = new JSONSerializer<Posting>(Posting.class, ctx);
      }
   
      @Override
      protected HTTPResponse executeInBackground() throws Exception {
         ArrayList<Posting> list = entityManager.readAll(select);
         JSONArray arr = jsonSerializer.serialize(list);
         return restClient.post("http://example.com", arr);
      }
   
   }

**TL;DR** DroidParts saves a lot of keystrokes & helps write elegant code.