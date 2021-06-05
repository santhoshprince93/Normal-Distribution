# Normal-Distribution
{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "5e89a245",
   "metadata": {},
   "outputs": [],
   "source": [
    "import pandas as pd\n",
    "import numpy as np"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "d3a4376d",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>Open</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Last</th>\n",
       "      <th>Close</th>\n",
       "      <th>Total Trade Quantity</th>\n",
       "      <th>Turnover (Lacs)</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2010-01-04</td>\n",
       "      <td>1121.0</td>\n",
       "      <td>1151.00</td>\n",
       "      <td>1121.00</td>\n",
       "      <td>1134.0</td>\n",
       "      <td>1135.60</td>\n",
       "      <td>101651.0</td>\n",
       "      <td>1157.18</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2010-01-05</td>\n",
       "      <td>1146.8</td>\n",
       "      <td>1149.00</td>\n",
       "      <td>1128.75</td>\n",
       "      <td>1135.0</td>\n",
       "      <td>1134.60</td>\n",
       "      <td>59504.0</td>\n",
       "      <td>676.47</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2010-01-06</td>\n",
       "      <td>1140.0</td>\n",
       "      <td>1164.25</td>\n",
       "      <td>1130.05</td>\n",
       "      <td>1137.0</td>\n",
       "      <td>1139.60</td>\n",
       "      <td>128908.0</td>\n",
       "      <td>1482.84</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2010-01-07</td>\n",
       "      <td>1142.0</td>\n",
       "      <td>1159.40</td>\n",
       "      <td>1119.20</td>\n",
       "      <td>1141.0</td>\n",
       "      <td>1144.15</td>\n",
       "      <td>117871.0</td>\n",
       "      <td>1352.98</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2010-01-08</td>\n",
       "      <td>1156.0</td>\n",
       "      <td>1172.00</td>\n",
       "      <td>1140.00</td>\n",
       "      <td>1141.2</td>\n",
       "      <td>1144.05</td>\n",
       "      <td>170063.0</td>\n",
       "      <td>1971.42</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "         Date    Open     High      Low    Last    Close  \\\n",
       "0  2010-01-04  1121.0  1151.00  1121.00  1134.0  1135.60   \n",
       "1  2010-01-05  1146.8  1149.00  1128.75  1135.0  1134.60   \n",
       "2  2010-01-06  1140.0  1164.25  1130.05  1137.0  1139.60   \n",
       "3  2010-01-07  1142.0  1159.40  1119.20  1141.0  1144.15   \n",
       "4  2010-01-08  1156.0  1172.00  1140.00  1141.2  1144.05   \n",
       "\n",
       "   Total Trade Quantity  Turnover (Lacs)  \n",
       "0              101651.0          1157.18  \n",
       "1               59504.0           676.47  \n",
       "2              128908.0          1482.84  \n",
       "3              117871.0          1352.98  \n",
       "4              170063.0          1971.42  "
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "beml_df = pd.read_csv(\"BEML.csv\")\n",
    "beml_df[0:5]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "id": "d7798e19",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>Open</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Last</th>\n",
       "      <th>Close</th>\n",
       "      <th>Total Trade Quantity</th>\n",
       "      <th>Turnover (Lacs)</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2010-01-04</td>\n",
       "      <td>1613.00</td>\n",
       "      <td>1629.10</td>\n",
       "      <td>1602.00</td>\n",
       "      <td>1629.0</td>\n",
       "      <td>1625.65</td>\n",
       "      <td>9365.0</td>\n",
       "      <td>151.74</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2010-01-05</td>\n",
       "      <td>1639.95</td>\n",
       "      <td>1639.95</td>\n",
       "      <td>1611.05</td>\n",
       "      <td>1620.0</td>\n",
       "      <td>1616.80</td>\n",
       "      <td>38148.0</td>\n",
       "      <td>622.58</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2010-01-06</td>\n",
       "      <td>1618.00</td>\n",
       "      <td>1644.00</td>\n",
       "      <td>1617.00</td>\n",
       "      <td>1639.0</td>\n",
       "      <td>1638.50</td>\n",
       "      <td>36519.0</td>\n",
       "      <td>595.09</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2010-01-07</td>\n",
       "      <td>1645.00</td>\n",
       "      <td>1654.00</td>\n",
       "      <td>1636.00</td>\n",
       "      <td>1648.0</td>\n",
       "      <td>1648.70</td>\n",
       "      <td>12809.0</td>\n",
       "      <td>211.00</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2010-01-08</td>\n",
       "      <td>1650.00</td>\n",
       "      <td>1650.00</td>\n",
       "      <td>1626.55</td>\n",
       "      <td>1640.0</td>\n",
       "      <td>1639.80</td>\n",
       "      <td>28035.0</td>\n",
       "      <td>459.11</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "         Date     Open     High      Low    Last    Close  \\\n",
       "0  2010-01-04  1613.00  1629.10  1602.00  1629.0  1625.65   \n",
       "1  2010-01-05  1639.95  1639.95  1611.05  1620.0  1616.80   \n",
       "2  2010-01-06  1618.00  1644.00  1617.00  1639.0  1638.50   \n",
       "3  2010-01-07  1645.00  1654.00  1636.00  1648.0  1648.70   \n",
       "4  2010-01-08  1650.00  1650.00  1626.55  1640.0  1639.80   \n",
       "\n",
       "   Total Trade Quantity  Turnover (Lacs)  \n",
       "0                9365.0           151.74  \n",
       "1               38148.0           622.58  \n",
       "2               36519.0           595.09  \n",
       "3               12809.0           211.00  \n",
       "4               28035.0           459.11  "
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "glaxo_df = pd.read_csv(\"GLAXO.csv\")\n",
    "glaxo_df[0:5]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "6c23eea3",
   "metadata": {},
   "outputs": [],
   "source": [
    "beml_df = beml_df[['Date', 'Close']]\n",
    "glaxo_df = glaxo_df[['Date', 'Close']]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "d0b2a043",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Date</th>\n",
       "      <th>Close</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>2010-01-04</td>\n",
       "      <td>1135.60</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2010-01-05</td>\n",
       "      <td>1134.60</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>2010-01-06</td>\n",
       "      <td>1139.60</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>2010-01-07</td>\n",
       "      <td>1144.15</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2010-01-08</td>\n",
       "      <td>1144.05</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>...</th>\n",
       "      <td>...</td>\n",
       "      <td>...</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1734</th>\n",
       "      <td>2016-12-26</td>\n",
       "      <td>950.25</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1735</th>\n",
       "      <td>2016-12-27</td>\n",
       "      <td>975.70</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1736</th>\n",
       "      <td>2016-12-28</td>\n",
       "      <td>974.40</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1737</th>\n",
       "      <td>2016-12-29</td>\n",
       "      <td>986.05</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1738</th>\n",
       "      <td>2016-12-30</td>\n",
       "      <td>1000.60</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>1739 rows × 2 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "            Date    Close\n",
       "0     2010-01-04  1135.60\n",
       "1     2010-01-05  1134.60\n",
       "2     2010-01-06  1139.60\n",
       "3     2010-01-07  1144.15\n",
       "4     2010-01-08  1144.05\n",
       "...          ...      ...\n",
       "1734  2016-12-26   950.25\n",
       "1735  2016-12-27   975.70\n",
       "1736  2016-12-28   974.40\n",
       "1737  2016-12-29   986.05\n",
       "1738  2016-12-30  1000.60\n",
       "\n",
       "[1739 rows x 2 columns]"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "beml_df"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "9142200b",
   "metadata": {},
   "outputs": [],
   "source": [
    "glaxo_df = glaxo_df.set_index(pd.DatetimeIndex(glaxo_df['Date']))\n",
    "beml_df = beml_df.set_index(pd.DatetimeIndex(beml_df['Date']))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "id": "a76d1795",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "import matplotlib.pyplot as plt\n",
    "import seaborn as sn\n",
    "%matplotlib inline\n",
    "plt.plot(glaxo_df.Close);\n",
    "plt.xlabel('Time');\n",
    "plt.ylabel('Close Price');"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "a1594f8c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.plot(beml_df.Close);\n",
    "plt.xlabel('Time');\n",
    "plt.ylabel('Close');"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "8e36e75d",
   "metadata": {},
   "outputs": [],
   "source": [
    "glaxo_df['gain'] = glaxo_df.Close.pct_change(periods = 1)\n",
    "beml_df['gain'] = beml_df.Close.pct_change(periods = 1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "8b033a50",
   "metadata": {},
   "outputs": [],
   "source": [
    "glaxo_df = glaxo_df.dropna()\n",
    "beml_df = beml_df.dropna()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "bdf64401",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAgAAAAF0CAYAAABVI4GwAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjMuNCwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8QVMy6AAAACXBIWXMAAAsTAAALEwEAmpwYAABaOklEQVR4nO3dedwd0/0H8M/3uc+TfZV9lSARIYuIWIPQIGgpVUJbLaVaqqrVRq21/CiqqKJpqZ2qUktil0iCkEUiErKIyCqL7PuznN8f9565c+fOzD0zd+7+eb9eeeV57jN37pm5s3znnO85R5RSICIiospSVegCEBERUf4xACAiIqpADACIiIgqEAMAIiKiCsQAgIiIqAIxACAiIqpABQ0AROREEZkvIotEZIzL388VkU8S/94XkUGm7yUiIiJvUqhxAEQkBmABgJEAlgOYBmC0UmqebZnDAXymlNogIqMA3KCUOsTkvW7at2+vevXqlZPtISIiKjYzZsxYp5Tq4Pa36nwXxmYYgEVKqcUAICLPADgVgHUTV0q9b1t+KoDupu9106tXL0yfPj2yDSAiIipmIvKV198K2QTQDcAy2+/LE695uQDAq0HfKyIXich0EZm+du3aLIpLRERUPgoZAIjLa67tESIyAvEA4PdB36uUGquUGqqUGtqhg2stCBERUcUpZBPAcgA9bL93B7DSuZCIDATwTwCjlFLfBHkvERERuStkDcA0AH1EpLeINAJwNoCX7AuISE8AzwP4oVJqQZD3EhERkbeC1QAopepE5FIArwOIAXhYKTVXRC5O/P1BANcBaAfgfhEBgLpEdb7rewuyIURERCWoYN0AC2Ho0KGKvQCIiKhSiMgMpdRQt79xJEAiIqIKxACAiIioAjEAICIiqkAMAIiIiCoQAwAiIqIKxACAiMqCUgqL1mwpdDGISgYDACIqC/+btQLfumsSJny+ptBFISoJDACIqCzMXbEZALBozdYCl4SoNDAAIKKyUDlDmhFFgwEAEZUFPaipuM0VSkRpGAAQERFVIAYAREREFYgBABERUQViAEBEZUExDZAoEAYARFQWkkmAzAIkMsEAgIjKCm//RGYYABAREVUgBgBEREQViAEAEZUVpgAQmWEAQERlQSn2AiAKggEAEZUVVgAQmWEAQEREVIEYABBRWWADAFEwDACIqKxwICAiMwwAiKgs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jj3bNS90MSgSlfkESHFWK16Fff/JcQBKJwJgEwARRWrInm0AAN3aNC1sQaggBJWZA1CKTQAFCQBEZA8ReVNEFib+T58eLr7ciSIyX0QWicgY2+s3iMgKEZmV+HdS/kqfOyUUOBJ5uviovfHGr4/CAd1aF7ooVACVmgTaKzHdecsmpVOxXqgagDEA3lZK9QHwduL3FCISA/A3AKMA9AcwWkT62xb5i1JqcOLf+HwUmogyq6oS9O3UstDFoAKRCu0FcOvpA/Dwj4din46lc+wXKgA4FcCjiZ8fBXCayzLDACxSSi1WSu0G8EzifUREVKQqNQmwWaNqHNuvU6GLEUihAoBOSqlVAJD4v6PLMt0ALLP9vjzxmnapiHwiIg97NSEAgIhcJCLTRWT62rVroyh7zlQnxlCtieX/a2nbrAZXjeqX988lovJyyYh9cML+nXDm0O6FLgplkLPGChF5C0Bnlz9dbboKl9d0UPkAgJsSv98E4M8AzndbiVJqLICxADB06NCiDkq/M7grFqzZgktG7JP3z/74uuPz/plEVH7at2iMv/9waKGLQQZyFgAopb7l9TcRWS0iXZRSq0SkC4A1LostB9DD9nt3ACsT615tW9c/ALwSTakLqyZWhatG7VfoYhARUQUoVBPASwDOS/x8HoAXXZaZBqCPiPQWkUYAzk68D4mgQfsugE9zWFYiKnMXH713oYtAlHeF6q9wG4BnReQCAEsBnAkAItIVwD+VUicppepE5FIArwOIAXhYKTU38f7bRWQw4k0ASwD8LM/lJ6IyMob5L1SBChIAKKW+AXCcy+srAZxk+308gLQufkqpH+a0gERERGWOIwESERFVIAYAREREFYgBABERUQViAEBERFSBGAAQERFVIAYAREREFYgBABERUQViAEBERFSBGAAQERFVIAYAREREFYgBABERUQViAEBERFSBGAAQERFVIAYAREREFYgBABERUQViAEBERFSBGAAQERFVIAYAREREFYgBABERUQViAEBERFSBGAAQERFVIAYAREREFai60AUgIiqUB38wBJt31hW6GEQFwQCAiCrWiQd0KXQRiAqGTQBEREQViAEAERFRBWIAQEREVIEYABAREVUgBgBEREQViAEAERFRBWIAQEREVIEYABAREVUgBgBEREQViAEAERFRBWIAQEREVIEYABAREVUgBgBE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\n",
      "text/plain": [
       "<Figure size 576x432 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.figure(figsize = (8, 6));\n",
    "plt.plot(glaxo_df.index, glaxo_df.gain);\n",
    "plt.xlabel('Time');\n",
    "plt.ylabel('gain');"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "id": "af6ce7f8",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\creat\\anaconda3\\lib\\site-packages\\seaborn\\distributions.py:2557: FutureWarning: `distplot` is a deprecated function and will be removed in a future version. Please adapt your code to use either `displot` (a figure-level function with similar flexibility) or `histplot` (an axes-level function for histograms).\n",
      "  warnings.warn(msg, FutureWarning)\n"
     ]
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "sn.distplot(glaxo_df.gain, label = 'Glaxo');\n",
    "plt.xlabel('gain');\n",
    "plt.ylabel('Density');\n",
    "plt.legend();"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "id": "45659788",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\creat\\anaconda3\\lib\\site-packages\\seaborn\\distributions.py:2557: FutureWarning: `distplot` is a deprecated function and will be removed in a future version. Please adapt your code to use either `displot` (a figure-level function with similar flexibility) or `histplot` (an axes-level function for histograms).\n",
      "  warnings.warn(msg, FutureWarning)\n"
     ]
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAX4AAAEGCAYAAABiq/5QAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjMuNCwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8QVMy6AAAACXBIWXMAAAsTAAALEwEAmpwYAAAnCklEQVR4nO3deZxbZ33v8c9PGmlmpNk3j/eJF2IHkjiJQxJCacpStqYhZWtYQi/QtPfCpZTbFtpbbuHS2xflQrdLyyVQLilLoNCUJECB4JIEmoU4wXHs2PG+jD327J5VMyPpuX9ImjjOjK2Z0dGRdL7v10svaY7O0flZnvnq0XOe8xxzziEiIsER8rsAEREpLgW/iEjAKPhFRAJGwS8iEjAKfhGRgKnyu4B8tLW1ua6uLr/LEBEpK48//ni/c6793OVlEfxdXV1s377d7zJERMqKmR2da7m6ekREAkbBLyISMAp+EZGAKYs+fhGRfMzMzNDd3U0ikfC7lKKqqalh1apVRCKRvNZX8ItIxeju7qa+vp6uri7MzO9yisI5x8DAAN3d3Vx00UV5baOuHhGpGIlEgtbW1sCEPoCZ0drauqBvOQp+EakoQQr9nIX+mxX8IiIBoz5+EalYX3/0WEFf723XrDnv8+FwmEsvvRTnHOFwmM9+9rO85CUv4ciRI2zevJmLL754dt0PfehD3HrrrXR1dbF69Wp++tOfzj63ZcsWkskku3bt4v777+fTn/403/3udwv271DwS9ma74/6Qn+cIl6pra1lx44dAPzwhz/kj//4j3nggQcAWL9+/exz5xodHeX48eOsXr2aPXv2eF6nunpERDwwMjJCc3NzXuu+5S1v4Zvf/CYAd955J7fccouXpSn4RUQKZXJyki1btrBp0ybe+9738tGPfnT2uYMHD7Jly5bZ29ldO29605u46667ALj33nu58cYbPa1TXT0iIgVydlfPww8/zK233squXbuA83f1tLS00NzczDe+8Q02b95MLBbztE61+EVEPHDdddfR399PX19fXuu/9a1v5X3ve5/n3TygFr+IiCf27t1LKpWitbWViYmJC65/880309PTw6tf/WpOnjzpaW0KfhGpWMUe4ZXr44fMVAp33HEH4XAYeLaPP+fd7343H/jAB2Z/rq+v58Mf/vCcr7tt2zZWrVo1+/O3vvUtrrvuukXXqeAXESmQVCo15/Kuri4mJyfnfO7IkSNzrp87NnDDDTfMu+1iqY9fRCRgFPwiIgGj4BeRiuKc87uEolvov1nBLyIVo6amhoGBgUCFf24+/pqamry30cFdEakYq1atoru7O++x85UidwWufCn4RaRiRCKRvK9CFWTq6hERCRgFv4hIwCj4RUQCRsEvIhIwCn4RkYBR8IuIBIyGc0pFcM7xrce7OTY4wfDkNL/9S+uIhNWuEZmLgl8qwhPHhtlxfJj2+mo+9YNn2Hn8DC97Qfvs87oAu8iz1CSSsjeamOG7O0/S1Rrn916xkXXtcR462E8qHZzT9kUWQsEvZW9n9xmmkmnesGUFITNeuqGNkUSSp06c8bs0kZKk4Jeyt/vkCJ0NNXQ0ZCapesGyetrqqnn4YL/PlYmUJs+C38xWm9lPzGyPme02s9/LLm8xs/vMbH/2vtmrGqTyjSZmODowziUrGmaXhczYsrqR7qFJJqaTPlYnUpq8bPEngf/mnNsMXAu8z8wuAT4CbHPObQS2ZX8WWZS9PaM44IVnBT/A+vY6HHC4f9yXukRKmWfB75zrcc49kX08CuwBVgI3AXdkV7sDeINXNUjle7pnhJZ4lM6G585FvrK5lkjYONin4Bc5V1H6+M2sC7gCeBRY5pzrgcyHA9Axzza3mdl2M9setLm1JT9p5zg6OM6G9jrM7DnPVYVCdLXGOdQ35lN1IqXL8+A3szrgX4APOudG8t3OOXe7c26rc25re3v7hTeQwOkbnSIxk2ZNS2zO59e119E7OsVoYqbIlYmUNk+D38wiZEL/a865u7KLT5vZ8uzzy4FeL2uQynVscAJg/uBviwPq5xc5l5ejegz4R2CPc+6vznrqHuBd2cfvAu72qgapbMcGJ4hFw7TWRed8fkVTLeGQcWJ4ssiViZQ2L6dsuB54J/CUme3ILvsT4JPAP5vZe4BjwJs9rEEq2LGBCVY3x57Xv58TDhnLGqrpOZMocmUipc2z4HfO/QyY+y8SXuHVfiUYhiem6RubYsuapvOut6Kxlqd7RnDOzfsBIRI0OnNXytKO48PA/P37Ocsba5iYTnF6ZKoIVYmUBwW/lKU9PaNApkV/PiuaMs/vPql5e0RyFPxSlvb0jNBUG6E2Gj7vep0NNRjw9Mm8RxKLVDwFv5SlPT0jdDbWXHC96kiYlniU3Qp+kVkKfik7iZkUh/rH8wp+gOVNtezuUVePSI6CX8rOgd4xUmnH8gv07+d0NlTTPTTJ5HTK48pEyoOCX8rO0z2ZbpvlDfm1+Nvra3AODmreHhFAwS9laE/PCLWRMC3znLF7rvb6akDBL5Kj4Jeys6dnhIs76wnleUJWWzxKyOBgr4JfBBT8UoYO9I5x8bL6vNevCodY0xLjgFr8IoCCX8rM8MQ0/WPTbOioW9B2GzrqOKAWvwjg7SRtIgXz9UePAXBsIDPF8vGhCTZ1Npxvk+dY31HHg/v6SabSVIXV3pFg01+AlJW+scycO+111Qvabn17HdOpNMeHNEWziIJfykrv6BThkNEcz29ET06ua0jdPSIKfikzfaNTtNVF8x7Rk7O+PRP8GtIpouCXMtM3OrXgbh6AxtoILfEoRwcmPKhKpLwo+KVsJFNphiamaa/P74zdc61tjXF0QNffFVHwS9kYGJ8m7Z49E3eh1rbE1OIXQcEvZaRvNDuiZ7HB3xrn5JlJppKarE2CTcEvZSM3lLMtzzl6zrW2NYZzcHxQQzol2BT8Ujb6RqdorI1QXXX+q27NZ21rHIBjg+rnl2BT8EvZ6BudWnQ3D0BXa+bC7Ef61c8vwabgl7LgnKNvbGnB3xKPUlddxbFBBb8Em4JfysJIIsl0Mr2oMfw5Zsba1hhHNKRTAk7BL2VhqSN6cta2xjimIZ0ScAp+KQt9owmgEMEf5/jQBKm0K0RZImVJwS9loW9siuqqEPXVS5tJvKs1xkzKcXJYQzoluBT8Uhb6RqfoqK/GFjg527nWtGSGdOoMXgkyBb+UhcysnEvr5gHoassO6dQBXgkwXYFLSt7kdIqRRJLWJQR/7gpeaeeoChk/3HWKkBlvu2ZNocoUKRtq8UvJy427b13kVA1nC5nREo8yMD695NcSKVcKfil5uW6Z1gVedWs+LfEogwp+CTAFv5S8o7PBv/Q+/szrRBkYn8I5DemUYFLwS8k7OjBBLBqmNrq4ydnO1VpXzUzKMTqVLMjriZQbBb+UvKMDE7QUqJsHmH2tgTF190gwKfil5B0ZGC9Y/z48e6xA/fwSVJ4Fv5l9ycx6zWzXWcs+ZmYnzGxH9vY6r/YvlWEqmeLk8OSShnKeqykWJWQwMD5VsNcUKSdetvi/DLxmjuV/7Zzbkr1938P9SwXoHpok7Qo3ogcgHDIaayMMqcUvAeVZ8DvnHgQGvXp9CYajBR7KmaMhnRJkfvTxv9/Mdma7gprnW8nMbjOz7Wa2va+vr5j1SQnJXS2rpYBdPQDNsSiDEzMFfU2RclHs4P8csB7YAvQAn5lvRefc7c65rc65re3t7UUqT0rN0YFx6quriBdoKGdOSzzK+FSSiWkN6ZTgKWrwO+dOO+dSzrk08AXgxcXcv5SfIwMTrG2LLXlWznPlhnQeH9T0zBI8RQ1+M1t+1o83A7vmW1cEMi3+ta3xgr9ucywX/JqeWYLHs9k5zexO4Aagzcy6gT8DbjCzLYADjgC/49X+pfzNpNJ0D03y+suWX3jlBcq1+HXhdQkiz4LfOXfLHIv/0av9SeU5OTxJMu1Y2xonmSrsvDqxaJhoVUjBL4GkM3elZB3JXiWry4OuHjOjJRale0jBL8Gj4JeSdSw7hr+rNebJ67fEo2rxSyAp+KVkHRmYoDYSpr2+sGP4c5pjEY4PTmp6ZgmcvILfzP7FzF5vZvqgkKLJjOgp/FDOnJZ4lMmZFP2apVMCJt8g/xzwNmC/mX3SzDZ5WJMIkB3D71E3D0CzRvZIQOUV/M65Hzvn3g5cSWYY5n1m9pCZ/Sczi3hZoARTKu04NjDhyYHdnJbsWH4d4JWgybvrxsxagd8C3gv8AvhbMh8E93lSmQTaqZEE06m0Jydv5cy2+AcU/BIseY3jN7O7gE3AV4AbnXM92ae+aWbbvSpOgutov7cjegAi4RAd9dUcV4tfAibfE7i+eO7c+WZW7Zybcs5t9aAuCbjcGP61bd61+AHWtMTUxy+Bk29Xz5/PsezhQhYicrajA+NEq0Isb6jxdD+rW2KaqE0C57wtfjPrBFYCtWZ2BZAbV9cAePcdXALvyMA4a1pihELeDOXMWd0S4+4dJ5hOpolWabSyBMOFunpeTeaA7irgr85aPgr8iUc1iXB0YMLT/v2c1c21pF1mXqAuj7uVRErFeYPfOXcHcIeZvdE59y9FqkkCzjnHkYFxrt/Q5vm+1rRkPlyOD00o+CUwLtTV8w7n3FeBLjP70LnPO+f+ao7NRJakd3SKxEy6KC3+J44NA/Dtx7tn+/rfds0az/cr4qcLdfXkmkB1XhciknM0N6LHwzH8OfU1VYRDxtC4rr8rwXGhrp7PZ+8/XpxyRDIHdsGb6ZjPFTKjORZhcELz9Uhw5DtJ26fMrMHMIma2zcz6zewdXhcnwXR0YJyqkLGiyduhnDnNsShD4wp+CY58T+D6VefcH5nZzUA38GbgJ8BXPatMAunrjx7jwX39NNZG+Oft3UXZZ0s8SvfQmaLsS6QU5DtwOTcR2+uAO51zgx7VI8LA+BStddGi7S83PXNiJlW0fYr4Kd/gv9fM9gJbgW1m1g4kvCtLgso5x8DYNC1xby6+Mpfm7Cydg+rukYDId1rmjwDXAVudczPAOHCTl4VJMI1Pp5hKpmmNF7fFDwp+CY58+/gBNpMZz3/2Nv9U4Hok4AbHpgCK2tWTa/EPaWSPBES+0zJ/BVgP7AByHaEOBb8U2EC21d1axK6e2miY2khYLX4JjHxb/FuBS5yuSi0eGxifxshcCL2YmuMRtfglMPI9uLsL6PSyEBGAgbEpmmIRqsLFnSmzJRZlUGfvSkDk2+JvA542s58DU7mFzrlf96QqCayB8emidvPktMSj7Dk1SlpfaiUA8g3+j3lZhEjOwNg0l65qLPp+m+NRUmnHaCJZ9H2LFFtewe+ce8DM1gIbnXM/NrMYEPa2NAmaofFpJmdSRR3KmdOisfwSIPnO1fPbwLeBz2cXrQS+41FNElCHs5OztdcVv6unOfthozl7JAjyPYL2PuB6YATAObcf6PCqKAmmw32Z4G/zIfibYhEMNEunBEK+wT/lnJv9i8iexKWjYFJQh/vHCdmzre9iqgqFaKyNqMUvgZBv8D9gZn9C5qLrrwK+BdzrXVkSRIf7x2mORQl7fIH1+TTHo2rxSyDkG/wfAfqAp4DfAb4P/KlXRUkwHeof96WbJ6dF8/JLQOQ7qidtZt8BvuOc6/O2JAmidNpxpH+cK9c0+VZDczzCSCJJYiZFTUSD1qRynbfFbxkfM7N+YC/wjJn1mdn/KE55EhSnRxNMzqRoq/exxZ89ttA9NOlbDSLFcKGung+SGc1ztXOu1TnXAlwDXG9mv3++Dc3sS2bWa2a7zlrWYmb3mdn+7H3zUv8BUhkO9/s3oicnN5b/+OCEbzWIFMOFgv9W4Bbn3OHcAufcIeAd2efO58vAa85Z9hFgm3NuI7At+7NISQR/bjTR8SEFv1S2CwV/xDnXf+7CbD//eadPdM49CJx7icabgDuyj+8A3pBfmVLpDveNUxMJUV+zkEtEFFZddRWRsHFsQMEvle1CwX++IQ6LGf6wzDnXA5C910lgAmRa/F2tcULmz1BOADOjORbliIJfKtyFmleXm9nIHMsNqPGgnmd3YHYbcBvAmjVrvNyVlIDD/eNsWl7vdxm01VVzNDt1hEilOm+L3zkXds41zHGrd84t5koZp81sOUD2vvc8+77dObfVObe1vb19EbuScjGTSnNscIKL2uJ+l0JrXZSjgxOk0zoxXSpXca92AfcA78o+fhdwd5H3LyWoe2iSZNpxUVud36XQFq9mOpnm5BkN6ZTK5Vnwm9mdwMPAxWbWbWbvAT4JvMrM9gOvyv4sAXe4fwygZFr8AEf61c8vlcuzIRTOuVvmeeoVXu1TytOh7Kyc69riPHNq1NdaWrPDSQ8PjPPSjW2+1iLilWJ39Yg8z+H+cZpiEV9m5TxXfU0VNZEQR/t1gFcql4JffHe4f7wkunkAQmZ0tcY5opE9UsEU/OK7Ugp+gK7W+OyZxCKVSMEvvpqYTtJzJsG6Ugr+tjjHBydJaUinVCgFv/jqQG9mRM+GDv+HcuZc1BZjOpXm5LCGdEplUvCLr/afzgT/xmX+n7Wbs6498yF0oG/M50pEvKHgF1/t7x0jEjbWtsT8LmXWhmzwH+xV8EtlUvCLr/afHmVdWx1V4dL5VWyOR2mNR2e7oUQqTen8tUkg7e8dY+Oy0unfz1nfUafgl4ql4BffTE6nOD40wcaO0unfz9nQUceBvjGc08geqTz+XfVCAu+zPzmAc3BqJMHXHz3mdznPsb69juGJGQbHp2encRCpFGrxi296RxIALPPxAuvzyQ0vVXePVCIFv/imd3SKsFlJtqhng19DOqUCKfjFN6fOJGirjxIO+Xe5xfmsaKwhFg2rxS8VScEvvjk1kmB5Y63fZczJzNjQUTd7gplIJVHwiy+GJ6Y5MzlDZ4Onl25ekk2d9ew9Ndclp0XKm4JffLGnJ3PBlc7GUg7+BvrHpukdTfhdikhBKfjFF7mW9PISDv7NyxuAZz+kRCqFgl98sadnhHg0TF116Z5Ksnl55sSyvT3q7pHKouAXX+zpGWV5Yy1mpTeiJ6cpFmV5Yw17FPxSYRT8UnTJVJp9p0dLun8/Z/PyBnX1SMVR8EvRHeofZyqZLun+/ZxNnfUc7BtjKpnyuxSRglHwS9E91X0GgBVNpTmG/2yblzeQTDuN55eKouCXonvqxBli0TDtJThHz7kuW9UIwM7sh5VIJVDwS9Ht7B7mRSsaCZXwgd2cNS0xmmIRnjw+7HcpIgWj4JeiSqbS7D45wqXZlnSpMzMuX9XEDgW/VBAFvxTV/t4xppLp2S6UcrBldRP7ekcZm0r6XYpIQZTu2TNSkXIHdl+0spFHDw36XM3czr0ozPDENM7BrhNnuHZdq09ViRSOWvxSVDtPDFNXXcVFrXG/S8nbquYYgLp7pGIo+KWonjg6zGWrGgmV4Bz884lXV9ESj7Lj2LDfpYgUhIJfimZsKsneUyNsXdvsdykLtrYlxmNHBnXxdakICn4pmiePD5N2cFVXi9+lLNhFbXEGxqd1RS6pCAp+KZrHjw5hlhklU27WtWeuwfvIoQGfKxFZOgW/FM3jR4d4QUc9jbURv0tZsOZYhBWNNTys4JcKoOCXokinHU8cG+LKMuzfh8yJXNeua+WRQ+rnl/Kncfziua8/eoxTZxKMJpLMpNLPGydfLq5d18pdvzjBvtNjXNxZ73c5IovmS/Cb2RFgFEgBSefcVj/qkOI51J85KHpRW/mM3z/X9RvbAHhwX5+CX8qan109v+Kc26LQD4aDfeO0xKM0x6J+l7JoK5tquXhZPdv2nva7FJElUR+/eC7tHIf7x1jfXr6t/ZyXb+7gsSNDnJmc8bsUkUXzK/gd8CMze9zMbptrBTO7zcy2m9n2vr6+IpcnhXRyeJLETHp2SGQ5e8WmDlJpx0/363dSypdfwX+9c+5K4LXA+8zsZeeu4Jy73Tm31Tm3tb29vfgVSsEc6hsHYF0Z9+/nXLGmmaZYhG17ev0uRWTRfAl+59zJ7H0v8K/Ai/2oQ4rjQO8YHfXV1NeU3/j9c4VDxss3dbBtz2ldh1fKVtGD38ziZlafewz8KrCr2HVIcYxNJTncP87FyypnFMyNl69gJJHkgWfU3SPlyY8W/zLgZ2b2JPBz4HvOuR/4UIcUwc/295FyjouXV07wv3RDGy3xKPc8edLvUkQWpejj+J1zh4DLi71f8ce/7+2lJhJibUv59+/nRMIhXndpJ99+vJvxqSTxap0HKeVFwznFM+m049/39rGxo55wGc2/n4+btqwkMZPm33ad8rsUkQVT8Itnnuwepn9sik0VeJbr1rXNrGuP89VHjvpdisiC6TuqeOZ7O3uIhI1NnQ1+l1IQ584xtLmzge891cOuE2d40cryuXi8iFr84ol02vHdnT388gs6qI2G/S7HE1euaaYmEuIrD6vVL+VFwS+e2H50iFMjCW68fLnfpXimNhrm5itW8q87TtA7kvC7HJG8KfjFE/c+eZKaSIhXbl7mdyme+p2XrSeZSvOFnx7yuxSRvKmPXwouMZPi7h0neOXmZRU/1PGhgwNctqqJLz90hPb6Guqy/963XbPG58pE5qcWvxTcvU+eZCSR5O3XrPW7lKK44QXtJFOO+5/R/D1SHhT8UnBfe/QYGzrquHZdi9+lFEVHQw1bu1p45NAAvaPq65fSp+CXgvrfP3iGHceH2dRZz50/P162l1lcqFddsoxIOMT3n+rRNXml5Cn4paDu35eZouHKNeV5UfXFqquu4pWbl7Hv9Bi/OD7sdzki56Xgl4J55tQou0+OcN26NmoilTl2/3yuW9/K2tYY3915kpPDk36XIzIvBb8UzN9t20+0KsT1G1r9LsUXITPedOUq0mn4r3f+gulk2u+SROak4JeCePTQAN97qoeXbmgjFq3sIZzn01pXzW9cuZLHjw7x8Xt3q79fSlJw/0KlYJKpNH92z25WNtXyso26TOZlq5porI3w+QcPsao5xn++Yb3fJYk8h4JfluyLPzvM3lOjfO7tVzI0MeN3OSXhw6/ZRM+ZBH/5g73U11TxjmuDcU6DlAcFvyzJrhNn+MyPnuG1L+rkNS/q5M6fH/e7pJIQChmffvPljE8l+dPv7MI5Rzg0d8+qzvKVYlMfvyzaSGKGD3zjF7TEo/zFzZdiVlkXW1mqaFWIf3jHlbxy8zI+evduHj7Y73dJIoCCXxYplXZ88Bs7ODYwwd+89Qqa41G/SypJ1VVh/uHtV/LqFy7j3p09/McBhb/4T109siif/tEz/PveXj5x0wu5bn0wh2+ez7lnLL90QzvdQ5N876ke0s7xSzoILj5Si18W7O4dJ/jc/Qe55cVrdNAyT+GQ8ZtXr+HSlY38265TPLivz++SJMDU4pcLOrv1emJ4ks8/cJCru5r5+K+/UP36CxAOGW/Zuhoz+MHuU6Sd44aLO/wuSwJIwS95G5tK8tVHjhKvruJVl3Ty7ce7/S6p7IRDxpuvWk3IjB89fZq0cxrVI0Wnrh7JSyrt+PqjxxifSvKOa9bOXnBEFi4cMt501SquWN3Ej/f08rn7D/pdkgSM/nolL997qocjA+O8+apVrGyu9bucshcy441XrSLlHH/5g73UVYd553VdfpclAaHglwvafmSQRw4N8NINbVwRsOmWvRSyTLdPR301H717N/HqKn7jylV+lyUBoK4eOa8njg1x95MnWd8e59Uv7PS7nIoTDhmffduVvGR9K3/47Z06biJFoeCXeR0fnOC2f9pOQ00Vt1y9hnBII3i8UBMJ84Vbt3Ltuhb+4FtP8n+27Sed1qye4h0Fv8xpJDHDu7/8GFPJNO+6rouYDuZ6Kl5dxZd+62pu2rKCz9y3j3ff8Rinzuj6veINBb88z0wqzfu+9gSH+8f5/DuuoqOhxu+SAqG6KszfvHULn3jDi3jo4AAv/8z9/PV9+xgYm/K7NKkwasbJcyRTaf7o2zv56f5+PvXGy3jJhjaODATjgul+OXd6h7AZP/79X+Yvvr+Hv922n889cJCXbWzjlZuX8fLNHXTU64NYlkbBL7MSMyk+9M87+P5Tp/jDV1/MW65e7XdJgbWmNcb/fedVHOgd5auPHOO+p0/z4z29AKxsqmVjRx0bl9WzpiXGO6/TtBmyMAp+AeDowDj/5WtPsPvkCH/6+s2895fW+V1SoJ39LeAFy+rZ2FHHqZEEe0+Nsu/0KA/u7+P+fX3Eq6vY3zvKr122gq1rmwnpALzkwcrhmqBbt25127dv97uMijSamOH//ccR/v4nBzCDt1y1mk3LG/wuSy5gcjrFgb4xnjpxhv2nR5lKpulsqOHXLlvOjZev4LJVjZpHSTCzx51zW5+3XMEfPMMT0/zi2DA/evo09z55krGpJK+7tJNLV2auFSvlZWomxZ5TozzVPcy+02OknKMlHuVNV63ihSsa2NhRz7r2ODWRsN+lSpHNF/zq6qkQo4kZPv/AIQbHpxmenGFyOsnkTIqO+hrOTM485zY4Pg1ALBrmVZcs493XX8Tlq5ued5BRykN1JMyW1U1sWd3E5HSKp3vOsLP7DF/62WGSZ50P0FYXJRoO0VAboaEmQkNtVfY+wi0vXkNnYw0NNVX6phAAvrT4zew1wN8CYeCLzrlPnm99tfifKzGTYvfJEXYcH87ehjg+OPmcdYzMiUG10TCxaJjaSJiaSOZxU22Elc0x1rbGiIQ1ordSJVNp+sem6R1N0Dc6xUhihpHJJCOJTANgYjr1vG1i0TDLG2tY0VTL8sYaljfWsqIpc7+soYamWITG2sjstwfnHMm0YzSRZGRyJnOfmGE0kXn9xtoILfEorfFqljfV6PetyEqmxW9mYeDvgVcB3cBjZnaPc+5pr/edTmd+SVNpR8o5kqk006k0UzNpppIpEjNpppKZx1PJZ5ensq0mMzBs9vFZ/ybsrGWGnfU4t9wIWaZ1Vl0Vyt7CVEee+zgaDmX3nWJiOkXf2BQ9ZxL0DE/yzKlRnu4ZYd/pUXINucbaCKuba7nkkgZa66ppiUdpjkWpjoQIqeUWaFXhEJ2NNXQ2zj38cyaVZjSR5MzkDJeuauT0mQQnz0zSM5ygZyTBjuOnGEskmatpWBUy0s6xkBOMQwbNsSiXr27iorY4XW1xLmqN01oXpbE284ESCYeoCtmCD1I753AO0s7hsv+2sakkE1MpxqaSjE8lGU0kGZ3KfPj97EA/iekUiWSKyZk0M8k0ZrCmJUY4u/+aqjB11WHi1VXEq6uom71/7rJYNIyZkU4/t4a0c7jse5Q+uz6XmaqjuipEdSRMNBya/duvrgoV5RuXH109LwYOOOcOAZjZN4CbgIIH//+892m+/vOjpLKBXwaHM86rs6GGS1Y00NlQw6rmWla1xGioUZ+8LE4kHKIlHqUlHmUskSReXcXGjno2dtTPrpNMpxmdTDI8mWnFT86kmJzONIxClmn0hMyojYSoyX6rzNxCRMIhEjOp2dAdHJ+mf2yKk8OTPHSwn8RM+rz1hUNG2IxQ9kuCc9kbzw3Yxf5dR8KZcK+JhIlUGc7Bzu4zsx9oyVSmITiTSj+ny8xr0XAILPNBaRi333pVwS/V6UfwrwSOn/VzN3DNuSuZ2W3Abdkfx8zsmSXutw0o9Stdn7fGo8CjxatlPuXwPkJ51KkaC6cc6lxUjS/78yXtc86TPPwI/rm+xzzv49Q5dztwe8F2arZ9rr6uUqIaC6cc6lSNhVMOdZZSjX4caekGzj4ldBVw0oc6REQCyY/gfwzYaGYXmVkU+E3gHh/qEBEJpKJ39Tjnkmb2fuCHZIZzfsk5t7sIuy5Yt5GHVGPhlEOdqrFwyqHOkqmxLM7cFRGRwtHZFCIiAaPgFxEJmIoJfjNrMbP7zGx/9r55nvW+ZGa9ZrbrnOUfM7MTZrYje3tdidaZ1/ZFqvE1ZvaMmR0ws4+ctdyz93K+fZ71vJnZ32Wf32lmV+a7bSEtsc4jZvZU9r3zbK6SPGrcZGYPm9mUmf3BQrYtkRqL8j7mWefbs//PO83sITO7PN9tPeGypxWX+w34FPCR7OOPAH85z3ovA64Edp2z/GPAH5RBnXlt73WNZA7MHwTWAVHgSeASL9/L8+3zrHVeB/wbmfNFrgUezXfbUqgz+9wRoM3j38N8auwArgb+19n/n8V6L5dSY7HexwXU+RKgOfv4tX78Xp59q5gWP5lpH+7IPr4DeMNcKznnHgQGi1TTXJZaZ17bL1E++5idesM5Nw3kpt7wUj77vAn4J5fxCNBkZsuLXO9S6iyWC9bonOt1zj0GzCx02xKosZjyqfMh59xQ9sdHyJy/lNe2Xqik4F/mnOsByN53LOI13p/9KvYlL7pQspZaZyH+nYXYx1xTb6w862cv3ssL7fN86+SzbaEspU7InMn+IzN73DJTl/hVoxfbLsRS91OM9xEWXud7yHzbW8y2BVFW8/Gb2Y+Bzjme+u8FePnPAZ8g88vyCeAzwLsX80Ie11kQBajxfFNvFOy9XMA+L7ROXlOFFMhS6gS43jl30sw6gPvMbG/2G2AhLeX9KNZ7udT9FON9hAXUaWa/Qib4X7rQbQuprILfOffK+Z4zs9Nmttw515P9yty7wNc+fdZrfQH4binWCSx1+0LVOO/UG4V8L/PdZx7rRPPYtlCWUifOudx9r5n9K5nugEIH1lKmTinWtCtL2k+R3kfIs04zuwz4IvBa59zAQrYttErq6rkHeFf28buAuxey8Tn9qzcDu+Zbd4mWVGcBti/UPuadesPD9zKf6T7uAW7Njpq5FjiT7a4q5lQhi67TzOJmVg9gZnHgV/Hmd3Ep70ex3stF76eI72NedZrZGuAu4J3OuX0L2dYTXh89LtYNaAW2Afuz9y3Z5SuA75+13p1AD5mDQd3Ae7LLvwI8BezMvvHLS7TOObf3qcbXAfvIjEr472ct9+y9nGufwO8Cv5t9bGQu9HMwW8PWC9Xr0f/zouokM7rjyextt5d15lFjZ/Z3bwQYzj5uKOZ7udgai/k+5lnnF4EhYEf2tt2P38vcTVM2iIgETCV19YiISB4U/CIiAaPgFxEJGAW/iEjAKPhFRAJGwS9SAGb2u2Z2q991iORDwzlFRAKmrKZsECkmM/so8HYyk2j1A48DZ4DbyEwBcYDMmZgTZvYxYMw592kzux94FPgVoInMyXc/Lfo/QGQe6uoRmYOZbQXeCFwB/AawNfvUXc65q51zlwN7yEy4NZcq59yLgQ8Cf+ZxuSILoha/yNxeCtztnJsEMLN7s8tfZGZ/TqYlXwf8cJ7t78rePw50eVemyMKpxS8yt7mmywX4MvB+59ylwMeBmnnWm8rep1ADS0qMgl9kbj8DbjSzGjOrA16fXV4P9JhZhEz/v0jZUUtEZA7OucfM7B4yszseBbaTObD7UTIHbo+SmVWz3rciRRZJwzlF5mFmdc65MTOLkbmAx23OuSf8rktkqdTiF5nf7WZ2CZl+/DsU+lIp1OIXEQkYHdwVEQkYBb+ISMAo+EVEAkbBLyISMAp+EZGA+f9WPDSdtWnSuwAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<Figure size 432x288 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "sn.distplot(beml_df.gain, label = 'BEML');\n",
    "plt.xlabel('gain');\n",
    "plt.ylabel('Density');\n",
    "plt.legend();"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "6b35358f",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Mean: 0.0004\n",
      "Standard Deviation:  0.0134\n"
     ]
    }
   ],
   "source": [
    "print('Mean:', round(glaxo_df.gain.mean(), 4))\n",
    "print('Standard Deviation: ', round(glaxo_df.gain.std(), 4))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "id": "0329d991",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Mean:  0.0003\n",
      "Standard Deviation:  0.0264\n"
     ]
    }
   ],
   "source": [
    "print('Mean: ', round(beml_df.gain.mean(), 4))\n",
    "print('Standard Deviation: ', round(beml_df.gain.std(), 4))"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "id": "231b68ef",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.06352488667177397"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "from scipy import stats\n",
    "stats.norm.cdf( -0.02,\n",
    "loc=glaxo_df.gain.mean(),\n",
    "scale=glaxo_df.gain.std())"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "id": "0d97bbe7",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.07104511457618568"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "1 - stats.norm.cdf(0.02,\n",
    "loc=glaxo_df.gain.mean(),\n",
    "scale=glaxo_df.gain.std())"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "ebb3851b",
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "_draft": {
   "nbviewer_url": "https://gist.github.com/8c951d7128653abf154acdc1f95d9f77"
  },
  "gist": {
   "data": {
    "description": "BEGL.ipynb",
    "public": true
   },
   "id": "8c951d7128653abf154acdc1f95d9f77"
  },
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.8.8"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
