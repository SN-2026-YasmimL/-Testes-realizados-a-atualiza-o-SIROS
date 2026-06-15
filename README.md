Link Pages

https://sn-2026-yasmiml.github.io/1-A-A-2Tri-YasmimL/



Mudei o fetch_flights.py

Desse:
print(f"\nRegistros filtrados para os aeroportos configurados: {len(registros)}")
print(
    "  Obs: o upsert usa constraint voos_unique "
    "(data_referencia + icao_empresa + numero_voo + icao_origem + icao_destino + etapa). "
    "Voos já existentes são atualizados — sem duplicatas."
)

Para: 
print(f"\nRegistros filtrados para os aeroportos configurados: {len(registros)}")

# Remove duplicados que quebram o upsert
registros_unicos = {}

for r in registros:
    chave = (
        r["data_referencia"],
        r["icao_empresa"],
        r["numero_voo"],
        r["icao_origem"],
        r["icao_destino"],
        r["etapa"],
    )

    registros_unicos[chave] = r

duplicados_removidos = len(registros) - len(registros_unicos)
registros = list(registros_unicos.values())

print(f"Duplicados removidos: {duplicados_removidos}")
print(f"Registros únicos: {len(registros)}")

print(
    "  Obs: o upsert usa constraint voos_unique "
    "(data_referencia + icao_empresa + numero_voo + icao_origem + icao_destino + etapa). "
    "Voos já existentes são atualizados — sem duplicatas."
)
