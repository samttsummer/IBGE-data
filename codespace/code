import requests
from bs4 import BeautifulSoup
import pandas as pd

def scrapeState(state: str) -> dict:
    stateUrl = f'https://www.ibge.gov.br/cidades-e-estados/{state}.html'

    response = requests.get(stateUrl)
    response.raiseForStatus()

    soup = BeautifulSoup(response.content, 'html.parser')
    indicators = soup.select('.indicador')

    stateData = {
        indicator.select_one('.ind-label').text.strip():
        indicator.select_one('.ind-value').text.strip()
        for indicator in indicators
    }

    return stateData

for indicator in stateData:
    if ']' in stateData[indicator]:
        stateData[indicator] = stateData[indicator].split(']')[0][:-8]
    else:
        stateData[indicator] = stateData[indicator]

stateData

stateDf = pd.DataFrame(stateData.values(), index=stateData.keys())
