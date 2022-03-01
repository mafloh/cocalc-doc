.. index:: Plot.ly
.. index:: Plotly
.. index:: Dash

.. highlight:: python

============================
Plot.ly's Dash Server
============================

.. _plotly-dash:

This is a simple example how to run `dash`_ by plot.ly in CoCalc.
This is taken from the `dash introduction <https://dash.plotly.com/layout>`_.

1. Create a file named ``dash_01.py``::

    import os
    import dash
    from dash import dcc
    from dash import html
    import plotly.express as px
    import pandas as pd

    # the next 4 lines are CoCalc specific
    port = 6767
    project_id = os.environ['COCALC_PROJECT_ID']
    base_url = f'/{project_id}/port/{port}/'
    dash_app = dash.Dash(name=__name__, url_base_pathname=base_url)

    # assume you have a "long-form" data frame
    # see https://plotly.com/python/px-arguments/ for more options
    df = pd.DataFrame({
        "Fruit": ["Apples", "Oranges", "Bananas", "Apples", "Oranges", "Bananas"],
        "Amount": [4, 1, 2, 2, 4, 5],
        "City": ["SF", "SF", "SF", "Montreal", "Montreal", "Montreal"]
    })

    fig = px.bar(df, x="Fruit", y="Amount", color="City", barmode="group")

    dash_app.layout = html.Div(children=[
        html.H1(children='Hello Dash'),
        html.Div(children='''
            Dash: A web application framework for your data.
        '''),
        dcc.Graph(id='example-graph', figure=fig)
    ])

    if __name__ == '__main__':
        print(f'Open this link to access Dash.')
        print(
            f'You might have to refresh once or twice in case it takes time to load!\n\n'
        )
        print(f'       http://cocalc.com{base_url}\n\n')
        dash_app.run_server(debug=True, port=port, host='0.0.0.0')



2. in a :doc:`../terminal` run::

        python3 dash_01.py

3. After 5-10 seconds of startup time, the interactive plot is accessible at the following URL::

        https://cocalc.com/[PROJECT_ID]/port/6767/

.. note::

    You might have to refresh the page once or twice to get it loaded up properly!

.. _dash: https://dash.plotly.com/
