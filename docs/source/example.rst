Example
========

This example shows how to use the class ``ExpMongoDBConnector`` of the module ``alfred3_dbtools.mongotools``.

.. note:: There needs to be at least one ``MongoSavingAgent`` added to your experiment.

.. code-block:: python
    :linenos:

    from alfred3_dbtools import mongotools

    from alfred3 import Experiment
    from alfred3.page import Page
    from alfred3.element import TextElement

    class Welcome(Page):
        def on_showing(self):
            db = self.experiment.db
            
            # query the first dataset for the experiment with title "dbtools Test"
            doc = db.find_one({"exp_title": "dbtools Test"}) 

            title = doc.get("exp_title", "No entry found in database.")
            start = doc.get("start_time", "No entry found in database.")
            
            # include title of query result in TextElement
            el = TextElement("Experiment: {exp}, started: {start}".format(exp=title, start=start)) 
            self.append(el)

    def generate_experiment(self, config=None):
        exp = Experiment(config=config)
        
        # initialise ExpMongoDBConnector
        db_connector = mongotools.ExpMongoDBConnector(exp) 
        
        # attaching the instance to the experiment instance facilitates availability from within pages (see line 9)
        exp.db = db_connector.db 
        
        welcome = Welcome(title="Welcome")

        exp.append(welcome)

        return exp


In this example, we have a one-page alfred experiment. 

1. The ``ExpMongoDBConnector`` is initialised right after the experiment. We attach a pointer to its ``db`` property to the experiment, so that we can easily access it from within pages. 
2. In the definition of the page ``Welcome``, we use the shortcut ``self.experiment.db`` to access the connector instance and perform a simple query, searching for the first document in the collection with a title of `"dbtools test"`. 
3. We then use a ``TextElement`` to display the content of this document's `exp_title` and `start_time` field on the page. 
