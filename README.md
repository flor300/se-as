[10:03 a. m., 14/11/2023] RL: public static IResult Buscar(string texto){
    var queryExpr = new BsonRegularExpression(new Regex(texto, RegexOptions.IgnoreCase));
    var filterBuilder = FilterDefinitionBuilder<LenguajeDbMap>();
    var filter = filterBuilder.Regex("Titulo",queryExpr) |
    filterBuilder.Regex("Description",queryExpr);

    BaseDatos bd= new BaseDatos();
    var coleccion=bd.ObtenerColeccion<LenguajeDbMap>("Lenguaje");
    var lista = coleccion = bd.Find(filter).ToList();
    
    return Results.Ok(lista);
    Id=x.Id.ToString(),
    IdCategoria=x.IdCategoria,
    Titulo=x.Titulo,
    Description=x.Description,
    EsVideo=x.EsVideo,.
    Url=x.Url
  }).ToList());
}
