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
[8:50 a. m., 14/11/2023] RL: import { Senia } from "./useSenias"
import React from "react"

interface Props{
    registros: Senia[],
    onEliminar: (item: Senia) => void
}

const ListadoSenias = ({ registros, onEliminar}: Props) => {
    const obternerUrlVideo = (registro: Senia) => {
        let url = "https://www.youtube.com/embed/";
        const idx = registro.Url.indexOf("?");
        const search = new URLSearchParams(registro.Url.substring(idx));
        url += search.get("v");

        return url;
    }
   return (
    <div className="container mt-4">
        <div className="row">
        {
            registros.map(x => 
                <div className="col-6 col-sm-4 col-lg-3 mb-3"  key={x.Id}>
                    <div className ="card h-100">
                        {
                            x.EsVideo
                            ?
                            <div className= "ratio ratio-16x9">
                                 <iframe src = {obternerUrlVideo(x)} allowFullScreen></iframe>
                            </div>
                            : <img src={x.Url} className="card-img-top"/>
                        }

                        <div className="card-body">
                            <h6>{x.Titulo}</h6>
                            <p>{x.Descripcion}</p>
                        </div>
                        <div className="card-footer">
                            <button className="btn btn-primary" onClick={()=> onEliminar(x)}>Eliminar</button>
                        </div>
                    </div>
                </div>
            )
        }
        {registros.length === 0 && <div className = "col-12"> No existe señas para mostrar. Agregar una imagen o un video de Youtube</div>}
        </div>
    </div>
   )
   }
export default ListadoSenias
[9:07 a. m., 14/11/2023] RL: import { Button, Modal } from "react-bootstrap";
import { Senia } from "./useSenias";
import React from "react";

interface Props{
    mostrar: boolean,
    onCerrarVentana: () => void,
    registro: Senia,
    dataChanged: (e: React.ChangeEvent<HTMLInputElement|HTMLTextAreaElement>)=> void,
    videoChanged: (e:React.ChangeEvent<HTMLInputElement>)=> void,
    onGuardar: ()=> void
}
export const AgregarSenias = ({ mostrar, onCerrarVentana, registro, dataChanged, videoChanged, onGuardar }: Props) => {

    return (
        <Modal show={mostrar} onHide={onCerrarVentana}>
            <Modal.Header closeButton>
            <Modal.Title>Nueva Seña</Modal.Title>
            </Modal.Header>
                <Modal.Body>
                    <div className="col-12">
 …
[9:31 a. m., 14/11/2023] RL: import { useEffect, useState } from "react";
import {useParams, useSearchParams} from "react-router-dom";

export interface Senia {
    Id: string,
    IdCategoria: string,
    Titulo: string,
    Descripcion: string,
    EsVideo: boolean,
    Url: string
}

export const useSenias= () => {
    const {idCategoria} = useParams();
    const [search, setSearch] =useSearchParams();

    const registroVacio : Senia = {
        Id: "",
        IdCategoria: idCategoria ||"",
        Titulo: "",
        Descripcion: "",
        EsVideo: false,
        Url: "" 
    };

    const [registro, setRegistro]= useState<Senia>(registroVacio);caches
    const [mostrar, setMostrar]= useState(false);
    const [senias, setSenias]=useState<Senia[]>([]);
    const [categoria, setC…
[10:03 a. m., 14/11/2023] RL: //////////////////////////////////////////////////////Actividad5
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
[10:05 a. m., 14/11/2023] RL: import { UseState } from "react";
import {FaSearch } from "react-icons/fa";

const Buscador = () => {
    const [textoBusqueda, setTextoBusqueda] = useState("");

    const onBusar = (e: React.KeyboardEvent<HTMLInputElement>) => {
        if(e.code === "Enter"){
            location.href = "/buscar?texto=" + textoBusqueda;
        }
    }

    return (
        <div className="container mt-4 mb-4">
           <div className="row">
              <div className="col-12">
                  <div className= "input-group input-group-lg">
                       <input type="text"
                            className="form-control"
                            placeholder="ingrese la seña a buscar y preciona Enter"
                            onKeyDown={onBuscar}
   …
[10:06 a. m., 14/11/2023] RL: import Buscador from "./Buscador";
import Menu from "./Menu";
import { SeniaBusquedaItene, useResultadoBuscar } from "./useResultadoBuscar";

const useResultadoBuscar = () => {
    const (texto, registros)=useResultadoBuscar();
    const obternerUrlVideo = (registro: SeniaBusquedaItene) =>
        let url = "https://ww.youtube.com/embed/";
        const idx =registro.Url.indexOf("?");
        const seaech = new URLSearchParams(registro.Url.substring(idx));
        url += seaech.get("v");

        return url;
    }
    return(
        <>
        <Menu />
        <Buscador/>
        <div className="container mt-4>
         <h5>Resultados de la busqueda <i>{texto}</i></h5>
         </div>
         <div className="container mt-4">
            <div className="row…
        public static IResult Buscar (string texto){
        var queryExpr=new BsonRegularExpression(new Regex(texto,RegexOptions.IgnoreCase));
        var filterBuilder= new FilterDefinitionBuilder<LenguajeDbMap>();
        var filter=filterBuilder.Regex("Titulo",queryExpr)|
        filterBuilder.Regex("Descripcion",queryExpr);

        BaseDatos bd= new BaseDatos();
        var coleccion=bd.ObtenerColeccion<LenguajeDbMap>("Lenguaje");
        var lista= coleccion.Find(filter).ToList();

        return Results.Ok(lista.Select(x=> new{
            Id=x.Id.ToString(),
            IdCategoria= x.IdCategoria,
            Titulo=x.Titulo,
            Descripcion=x.Descripcion,
            EsVideo=x.EsVideo,
            Url=x.Url
        }).ToList());
    }

